---
title: "Sensemaker"
---

[Sensemaker | Jigsaw](https://jigsaw-code.github.io/sensemaking-tools/)
[[Jigsaw Sensemaker]]
[[Jigsaw]]

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Google JigsawのSenseMakerがどういうアルゴリズムか解説して
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>了解。要点だけ手短にまとめます。

Jigsawの「Sensemaker」のアルゴリズム概観
目的
大量の自由記述（コメント）と投票（賛成・反対・パス）を、話題構造と合意/対立パターンに整理し、物語調の要約と図表に落とすためのツールキット。Google Cloud Vertex AI（主に Gemini）上で動くオープンソース実装です。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools?utm_source=chatgpt.com))

処理パイプライン（3段）
1. [[Topic Identification]]（[[話題同定]]）
    - LLMを用いて、コメント群に含まれるトピック→サブトピック→**テーマ（必要ならサブサブトピック）**までの階層を可変に抽出。教師なしの「話題見立て」をまず作る段です（深さは設定で調整）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
2. [[Statement Categorization]]（[[発言の多ラベル分類]]）
    - 各コメントを、上で定義した複数のトピック/サブトピックに多ラベルで割り当て。
    - 出力の信頼性を上げるため、Vertex AI の “constrained decoding” を使い、事前定義のJSONスキーマに沿ったフォーマットのみをLLMが生成できるよう制約（フォーマット崩れ対策&自動リトライを実装）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
3. Summarization（要約・合意/相違の抽出）
    - 最終レポートを生成。
        - Themes: 各サブトピックで頻出の論点（最大5つ）をテキスト内容のみから要約（投票は使わない）。
        - Common Ground / Differences of Opinion: 投票データを統計的に見て、賛成率/反対率のシグナルが明確な発言をサンプリングし要約。投票総数が20未満の発言は除外して誤判定を抑制。
        - Relative Agreement: サブトピックごとに「高/中高/中低/低の合意度」を、そのサブトピック内で“共通基盤”に入った発言数の比率をベースに相対評価。
        - レポートは**根拠として元発言と票数への参照（citation）**を付与可能。
        - さらに全体のOverviewやTop 5 Subtopicsなど、段階的に集約した見出し要約を生成（内部では段階要約=“chain-of-thought的中間生成”を用いる）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))

モデル/実装まわり
- 既定は Vertex AI の Gemini 1.5 等を利用。ただしModel Garden経由で Gemma/Llama/Claude などに差し替え可能。独自モデルもシンプルな Model 抽象（テキスト生成・構造化生成の2メソッド）を実装すれば利用可。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- 規模感の目安：コメント**~1000件**で、話題同定・分類・要約トータルのトークン見積りとコスト例（2025-04-10時点、Gemini 1.5 Proで合計1ドル未満という目安を提示）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- 安定性検証：再実行時の安定度は、**コメントのカテゴリ一致が約90%**と記載（シルエット係数に基づく評価コードは公開予定）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- GitHub: ランナーCLI、再実行比較（rerunner）、可視化ドキュメントも公開。Issue欄にはJSON整形/カテゴリ分割等の改善提案も。([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools?utm_source=chatgpt.com))

出力の特徴（現場適用での見え方）
- 合意/相違の地図化：どこが「共通基盤」か、どこに「対立軸」があるかを、投票シグナルで明示。
- 人間の判断を補助：Kentuckyの大規模タウンホールや「We The People」全国対話で運用され、自治体や主催側が短時間で論点整理できた事例が紹介されています。([Medium](https://medium.com/jigsaw/how-one-of-the-fastest-growing-cities-in-kentucky-used-ai-to-plan-for-the-next-25-years-3b70c4fd1412?utm_source=chatgpt.com))

Polis 等とのちがい（かんたん比較）
- 共通点：自由記述＋賛否投票→クラスタ別の合意/不合意を可視化する点。
- Sensemakerの色：
    - LLMを全面活用し階層トピック化と物語要約を標準化（constrained decodingで構造化出力）。
    - 合意/相違の抽出はテキスト解析ではなく投票統計でサンプリング→要約、というデータ駆動の分離設計。
    - Vertex AI上でモデル可換・ツールキット指向（他プラットフォームから吐き出されたCSVでも回せる）。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))

参考リンク（公式と一次情報中心）
- ドキュメント（How it works/評価/コスト/コード例）([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
- GitHub（コード・ランナーCLI・可視化・Issues）([GitHub](https://github.com/Jigsaw-Code/sensemaking-tools?utm_source=chatgpt.com))
- 事例記事（Bowling Green、We The People）([Medium](https://medium.com/jigsaw/how-one-of-the-fastest-growing-cities-in-kentucky-used-ai-to-plan-for-the-next-25-years-3b70c4fd1412?utm_source=chatgpt.com))
- コンセプト解説（Medium）([Medium](https://medium.com/jigsaw/making-sense-of-large-scale-online-conversations-b153340bda55?utm_source=chatgpt.com))

ひとこと評価（実務視点）
- 強み：スケール（数千〜）でも階層構造と“合意/相違”を短時間で提示。出力をJSON制約で整形しやすい。
- 注意：投票母数20未満は除外など、シグナル強度に依存。入力設計（質問の切り方・投票設計）と人間のレビューは依然重要。([jigsaw-code.github.io](https://jigsaw-code.github.io/sensemaking-tools/docs/))
必要なら、サンプルCSV（Polis形式や独自アンケート）を渡してもらえれば、Sensemaker流のトピック階層＋合意/相違サマリーのダミー出力をこちらで作って見せます。

