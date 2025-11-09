---
title: "pSensemaker2025-10-21"
---

from [[Jigsaw Sensemakerとtttc-light-js勉強会]]
pSensemaker2025-10-21
[[DeepWiki]]
[https://deepwiki.com/Jigsaw-Code/sensemaking-tools](https://deepwiki.com/Jigsaw-Code/sensemaking-tools)

[[SensemakerにYouTubeの高評価だけ入れたらどうなる？]]
- いまいち
- 投票データがないときはだいたいTalk to the City Turboと同じ

repoのコードはGemini-2.5-previewを使っていたのでGemini-2.5でここまでの実験をしたが1.5でいいのかもな

クラスタリング結果をUMAPして観察
- 予想としてはランダムでもないが明瞭分離でもないものになる
- [[高次元空間でクラスタリングしてからUMAP]]
カテゴリのembeddingをconcatする実験
- [[クラスタ解説の埋め込みベクトルをconcatしてUMAP]]

[[Supervised UMAP]]で要件を満たすか試せってGPT5が言ってた
- 僕が考えてた二段階アプローチは要件を満たさなかったときに考えろってさ
- [https://chatgpt.com/c/68f5f6ca-2178-8323-835c-43f0a2ba772d](https://chatgpt.com/c/68f5f6ca-2178-8323-835c-43f0a2ba772d)

Polisも日本語化プロンプトで実行
[https://gist.github.com/nishio/1328c4ca664b56c31ec30dfde8c6cda7](https://gist.github.com/nishio/1328c4ca664b56c31ec30dfde8c6cda7)
- 8 topics 27 subtopics
英語だと同じデータで
- 4 topics 14 subtopics
だったのにね


tttc-light-js
[https://deepwiki.com/AIObjectives/tttc-light-js](https://deepwiki.com/AIObjectives/tttc-light-js)
入力データはid,textでよさそう
test_pipeline.pyを使えば、Webサーバーを立ち上げずにパイプラインを直接実行できます。

JigsawでYouTubeコメントから投票データを取り除いたものを実行中
- [https://gist.github.com/nishio/34bb875cbe1147f8a95ca9b8ee0a0ba2](https://gist.github.com/nishio/34bb875cbe1147f8a95ca9b8ee0a0ba2)
- あ、gemini-1.5にするつもりだったのにすっかり忘れてた

同一データをtttc-light-jsでも実行中
- 50件のテストが成功しました。以下のトピックが抽出されました：
    1. AI and Creativity - AIが創造性に与える影響
    2. Public Consultation Tools - Polisなどの公開協議ツール
    3. Democracy and Plurality - 民主主義と多元性
    4. Cultural Perspectives - 文化的視点
    5. Economic Implications - 経済的影響
- 全1105件のコメントを処理しますか？時間はかかりますが（おそらく15-30分程度）、より包括的な分析結果が得られます。
- > 22.24s user 2.18s system 4% cpu 8:11.49 total
    - 全然そんなにかからないよ
    - 0.3$くらいだな
- [https://gist.github.com/nishio/9b7466f848f72be29f8eb7f817012c26](https://gist.github.com/nishio/9b7466f848f72be29f8eb7f817012c26)

:

```
投票データなしでも以下の主要な3つの処理は正常に動作します：

  1. トピック識別 (Topic Identification)
    - コメントからトピック、サブトピック、テーマを自動学習
    - コード: library/src/tasks/topic_modeling.ts
  2. 分類 (Categorization)
    - 各コメントを学習したトピックに分類
    - コード: library/src/tasks/categorization.ts
  3. 要約生成 (Summarization)
    - テーマベースの要約を生成
    - コード: library/src/tasks/summarization.ts

  投票データなしで生成される内容

  要約レポートには以下が含まれます：

  - Introduction: コメント数、トピック数、サブトピック数の統計
    - コード: library/src/tasks/summarization_subtasks/intro.ts:22-39
  - Overview: 会話全体の概要
    - コード: library/src/tasks/summarization_subtasks/overview.ts
  - Top Subtopics: コメント数が多い上位5つのサブトピック
    - コード: library/src/tasks/summarization_subtasks/top_subtopics.ts
  - Prominent Themes (各トピックごと): テキストのみから抽出されたテーマ
    - コード: library/src/tasks/summarization_subtasks/topics.ts:330-363

  以下の分析は投票データに依存するため、空または省略されます：

  - Common Ground (共通認識): 高い賛成率のコメント
    - コード: library/src/tasks/summarization_subtasks/topics.ts:369-397
    - 判定: library/src/stats/summary_stats.ts:55-67でfilteredCommentsが空になる
  - Differences of Opinion (意見の相違): 賛否が拮抗するコメント
    - コード: library/src/tasks/summarization_subtasks/topics.ts:403-436
  - Groups (グループ分析): グループ間の意見の違い
    - コード: library/src/tasks/summarization_subtasks/groups.ts

  重要なコードの場所

  library/src/
  ├── sensemaker.ts              # メインAPI (summarize, learnTopics, categorizeComments)
  ├── stats/
  │   ├── summary_stats.ts:55-67 # filteredComments作成 (投票データチェック)
  │   └── majority_vote.ts       # 投票ベースの統計計算
  └── tasks/
      ├── summarization.ts:44-51 # 投票データの有無で統計クラスを選択
      └── summarization_subtasks/
          ├── intro.ts:26-27     # 投票数の表示 (0票と表示される)
          └── topics.ts:330-363  # Themesは投票データなしでも生成される
                       :369-436  # Common Ground/Differencesは空になる

  つまり、投票データなしでもテーマ抽出と構造化された要約は生成されますが、コンセンサスや意見の相違の分析は行われません。
```


- LLMベースで行った分類は高次元embeddingベースではどう見えるのか？
    - tttc-light-jsで試す？

from [[dd2030 slack]]
[[AffinityBubble]]の文脈から

中山心太（tokoroten）
「問題の全体像を素早くつかむ」に特化させるとこれが正解ぽいよね

NISHIO Hirokazu
散布図を欲しがるユーザ、実際のところ散布図が欲しいわけではない、という
欲しいものが言語化できてなくて散布図を見せられて「おっこれが欲しい」となってるけど、たぶん本当に欲しかったものは散布図ではない

中山心太（tokoroten）
「AIを使っている我々」と「AIを使っている彼ら」　であれば、散布図が合致する
「安いコストでSNS映えする分析結果を作成して、インプレッションを作成する」
データ分析初心者は、データ分析からナラティブを発してくれる装置が欲しい

分析結果に対して、質問できるようにするとどうなるんだろう。

AIと会話しながら、集計、分類、要約、インサイトを交互にぐるぐる回し続けるような仕組みがよさそうだなぁ。
BigQueryにGeminiにクエリを作らせる機能があるように、その延長線で。

GPTsやNoteBookLM用のデータに変換する、というのがいい気がしてきた

NISHIO Hirokazu
まあ、それを言い出すと大部分のユースケースではデータをNotebookLMに突っ込めば良くない？
1000件の自由記述くらいコンテキストに入る

中山心太（tokoroten）
あれは、一次データをそのまま取り扱うしかできないので、
まぁ、そうか、コンテキストが長いからできるか。

NISHIO Hirokazu
AIと会話しながら、集計、分類、要約、インサイトを交互にぐるぐる回し続けるような仕組みがよさそう
この運用が有用であることに関しては賛成

> 大部分のユースケースではデータをNotebookLMに突っ込めば良くない？

でもこれ、NotebookLMの実装がどうなってるか知らんけどコンテキストに積んでの単発のLLM呼び出しではマルチヘッドアテンションのヘッドの数で抽出できる地検が制約されそうな気はするね
TTTC Turbo的手法で作ったクラスタ要約を積んであげた方が良い結果が出やすそうではある

でもこれ、ちゃんとReasoningできるモデルを使えばいいだけではという気もして、結論ChatGPTに課金してコンテキストにデータを置いてしっかりThinkingさせようということになる気もしてきた
コンテキストに乗らない場合でもGPTsでRAGさせればいいだけな気もするしなぁ、深掘りさせたければネット検索させることもできるし。安いAIでなんとかしようとすることが不毛な気がしてきたな……

いまSenseMakerとtttc-turbo-jsに入れて試してたデータをChatGPT５Thinking にも入れてみてる

