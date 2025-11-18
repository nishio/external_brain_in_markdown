---
title: "Jigsaw SenseMaker"
---

[[Google Jigsaw Sensemaker]]
- [[SenseMaker]]



<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
[[Jigsaw]]の「[[Sensemaker]]」は、大規模な会話データ（例: Polis）をAIで「分類・要約・合意/相違の可視化」までやるオープンソースのツールキットです（現在β）｡ ([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools))

クイックスタート（ローカル実行）
1. 取得
bash

```
git clone https://github.com/Jigsaw-Code/sensemaking-tools
cd sensemaking-tools
npm i
```

（ライブラリ一式はGitHub公開）｡ ([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))

2. Vertex AI 認証（デフォルトはGeminiをVertex経由で使用）
bash

```
gcloud config set project <YOUR_GCP_PROJECT>
gcloud auth application-default login
```

※ 他モデルへの差し替えも可（Model Garden・独自モデル）｡ ([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))

3. サンプルCSVを用意
Polisのオープンデータ「15-per-hour-seattle」を落として手元に置きます。 ([GitHub](https://github.com/compdemocracy/openData?utm_source=chatgpt.com))

4. とりあえず要約HTMLを出す
ヘルプを見て実行（実行時引数は `--help` で確認）:
bash

```
npx ts-node library/runner-cli/runner.ts --help
# 例: 入力CSV→要約HTML（出力先や引数は--help参照）
```

このランナーは「CSVを読み, 要約入りHTMLを生成」する簡易CLIです｡ ([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))

5. もっとリッチに（インタラクティブWebレポート）
- まず上級ランナーで3つのJSONを出力（topics / comments+scores / summary）。
- その後 Web UI をビルド:
bash

```
cd web-ui
npx ts-node site-build.ts \
  --topics   <path-to-topics.json> \
  --summary  <path-to-summary.json> \
  --comments <path-to-comments.json> \
  --reportTitle "My Report"
npm run dev  # http://localhost:4200
# 1ファイルHTMLが良ければ:
npx ts-node single-html-build.js
```

（ビルド手順は公式READMEに明記）｡ ([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))

自分のデータで回す（Polis想定）
- 必須列: `comment_text`, `comment-id`
- 票がある場合: `agrees`, `disagrees`, `passes`
- グループ別の票がある場合: `{GROUP}-agree-count`, `{GROUP}-disagree-count`, `{GROUP}-pass-count`
この形式のCSVを入れるだけでOKです。 ([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools))
※ 公式How-toでも「現状はPolis形式をサポート」と明記。

モデル/コスト/注意
- 既定: Vertex AI の最新Gemini。Model Gardenの他モデルや独自モデルにも差し替え可能（抽象`Model`で実装）｡ ([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- 目安コスト（約1000件の発言）: 入出力トークン合計は概ねこの程度で、2025-04-10時点ではGemini 1.5 Proで総額$1未満の例が記載。実コストは価格表を要確認。 ([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- ライブラリはβ段階。出力の安定性や根拠表示（引用ホバー）などの設計もドキュメント化。 ([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))

出力イメージ
KentuckyのBG2050プロジェクトの公開レポート（インタラクティブ）で雰囲気が掴めます。 ([What Could BG Be?](https://report.whatcouldbgbe.com/))

西尾さんの次の一手（最短ルート）
- まずサンプルCSVで `runner.ts` を回しHTMLを1枚出す
- すぐにPolisのエクスポートCSV（上記列名）で同手順→必要ならWebレポ化（`site-build.ts`）


[[Topic Identification]]（トピック抽出）
- LLMに抽出させる方式。会話全体のテキストから、
- ①トップレベルのみ／②トップ＋サブトピック／③既定トピックを与えてサブのみ、の3モードで階層を生成できます。
- 実装的には learnTopics(comments, includeSubtopics, existingTopics?, context?) の形で呼び出し（ドキュメントのサンプル）。
- 安定性評価はシルエット係数等で検討中、ラン間の一致 ~90% との報告（評価コードは近日公開予定）。
- [sensemaking-tools/library/src/tasks/topic_modeling.ts at main · Jigsaw-Code/sensemaking-tools](https://github.com/Jigsaw-Code/sensemaking-tools/blob/main/library/src/tasks/topic_modeling.ts)

[[Statement Categorization]]（発言の割当）
- マルチラベル割当。抽出済み（またはユーザ定義）トピックへ各発言をバッチで分類します。
- Vertex AIの“constrained decoding”でJSONスキーマを強制し、LLM出力の型崩れを抑制。失敗時はリトライを実装。
- CLI でも同等の処理があり、カテゴリ割当だけのランナー（categorization_runner.ts）も提供。
- [sensemaking-tools/library/src/tasks/categorization.ts at main · Jigsaw-Code/sensemaking-tools](https://github.com/Jigsaw-Code/sensemaking-tools/blob/main/library/src/tasks/categorization.ts)

---
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Polis的に各個人の投票データを持って相関を計算するのではなく、個々の質問ごとに賛否の割合のデータとして要約して、合意が多いか少ないかの1次元の尺度として使う？
<img src='https://scrapbox.io/api/pages/nishio/gpt5/icon' alt='gpt5.icon' height="19.5"/>はい、その理解でほぼOKです。
- Sensemakerは個人×発言の投票ベクトルから相関やクラスタを作る（PolisのOpinion Groups型）ことはせず、各発言の賛成/反対/パスの集計比率だけで「Common Ground（合意）／Differences of Opinion（相違）」にふさわしい発言を選びます。小標本は誤解を避けるため総票数20未満を除外。テキストは「トピック抽出・割当」にのみ使い、合意/相違の選定自体には使いません。
- さらに、Relative Agreement（相対合意度）は「各サブトピックで“Common Groundに入った発言数/そのサブトピック内の発言総数”を他サブトピックと相対比較」して High/Low を付ける――つまりここでも事実上1次元の“合意の強さ”指標として扱われます。
