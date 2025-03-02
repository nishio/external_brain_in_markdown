---
title: "MemoChat: Tuning LLMs to Use Memos for Consistent Long-Range Open-Domain Conversation"
---

> We propose MemoChat, a pipeline for refining instructions that enables large language models (LLMs) to effectively employ self-composed memos for maintaining consistent long-range open-domain conversations. We demonstrate a long-range open-domain conversation through iterative "memorization-retrieval-response" cycles. This requires us to carefully design tailored tuning instructions for each distinct stage. The instructions are reconstructed from a collection of public datasets to teach the LLMs to memorize and retrieve past dialogues with structured memos, leading to enhanced consistency when participating in future conversations. We invite experts to manually annotate a test set designed to evaluate the consistency of long-range conversations questions. Experiments on three testing scenarios involving both open-source and API-accessible chatbots at scale verify the efficacy of MemoChat, which outperforms strong baselines. Our codes, data and models are available here: this https URL.
(DeepL)我々は、大規模言語モデル(LLM)が一貫した長距離オープンドメイン会話を維持するために、自己合成メモを効果的に使用することを可能にする、命令を洗練するためのパイプラインであるメモチャットを提案する。我々は、「記憶-検索-応答」サイクルの繰り返しによる長距離オープンドメイン会話を実証する。そのためには、各段階に合わせた調整命令を注意深く設計する必要がある。LLMが過去の対話を構造化されたメモで記憶し、検索することを教え、将来の会話に参加する際の一貫性を高める。我々は、長距離会話質問の一貫性を評価するために設計されたテストセットに手動で注釈を付けるよう専門家に依頼する。オープンソースとAPIアクセス可能なチャットボットの両方を含む3つのテストシナリオの実験では、強力なベースラインを上回る[[MemoChat]]の有効性が検証されました。私たちのコード、データ、モデルは、こちらのhttps URLから入手できます。

> [ai_database](https://twitter.com/ai_database/status/1692403982734594175/photo/1) LLMが”わたしの話”を①体系的なメモで長期的に記憶し、②必要に応じて思い出し、③レスポンスを送るようにするパイプライン「MemoChat」が開発されました。
>
>  テンセントなどの研究者グループが発表しています。
>  ○ Junru Lu et al. MemoChat: Tuning LLMs to Use Memos for Consistent Long-Range Open-Domain Conversation
>
>  現在のLLMチャットボットは、会話が長くなってきた時に”一貫したレス”を返すことが苦手です。
>
>  そこで研究者らは、多様なトピックを含む長い会話でも「構造化されたメモ」を作らせることで解決しようとしています。
>
>  以下は方法論のまとめです。すべてLLM側の動作です。
>  ■会話をトピックごとに細分化し、メモを書く
>  ■新しい会話のクエリに応じてメモを見返す
>  ■現在の話と過去の話を照らし合わせながらレスする
>
>  実験では、4つのオープンソースLLMに対して上回る性能を出しました。
>
>  大規模なリソースから弾き出される「中立的な回答」を行う複雑なチャットボットではなく、とにかく”わたしの話”に応じた会話をしてほしい際に有用な技術です。

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文は、長期の開放領域の会話において、大規模言語モデル(LLM)がメモを用いて一貫した応答を行えるようにするためのMemoChat手法を提案しています。主な内容は以下の通りです。
- MemoChatは、「メモ化」「検索」「応答」のループを通じて、長期の会話を行うことを目指す。これによって、過去の会話内容を構造化されたメモとして保存し、必要に応じて検索・参照することで一貫性のある応答が可能になる。
- 公開データセットを再構築し、オープンソースのLLMをMemoChat手法に適するようファインチューニングするための指示データを作成した。
- 長期会話の一貫性評価のために、専門家によるアノテーションを行った評価用データセットを新たに作成した。
- 公開APIを通して利用可能なチャットボットおよびオープンソースのLLMを用いて評価実験を行い、MemoChatの有効性を確認した。
- 実験では、大規模なLLMほど zero-shot/few-shot でのメモの利用能力が高く、指示データによるファインチューニングでさらに性能が向上することが示された。

以上のように、MemoChatは構造化メモの自律的な利用によって、LLMによる長期の開放領域の会話を実現する手法であると言えます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>トピックによるチャット範囲の分割はどうやってる？
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/> 論文では、会話をトピックに基づいて分割するために、以下のようなタスク指示(Memo Writing Instruction)をLLMに与えています。

1. 会話中のすべての可能なトピックを簡潔な語句(spans)で要約する。
2. 各トピックのチャット範囲を決定する。これらの範囲は、重複のない、順番につながった端から端までの区間の集合であるべき。
3. 各チャットの要約を短い文で結論付ける。
4. トピック、要約、範囲の結果をJSONフォーマットで、'topic', 'summary', 'start', 'end'のキーを使って報告する。

例えば、M行の会話が1行目からN行目まで「バナナ」について話し、N+1行目からM行目まで「マンゴー」について話す場合、タスクの結果は以下のようになります。

[{'topic': 'banana', 'summary': 'user talks banana with bot.', 'start': 1, 'end': N},
{'topic': 'mango', 'summary': 'bot brings mango for user.', 'start': N+1, 'end': M}]

このようなタスク指示をLLMに与え、教師あり学習することで、LLMが自律的に会話をトピックごとに分割し、各トピックの要約と範囲を出力できるようにしているのです。これによって会話履歴の構造化が可能になります。