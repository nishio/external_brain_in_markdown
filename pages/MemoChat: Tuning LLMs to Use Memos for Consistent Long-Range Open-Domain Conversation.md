
> We propose MemoChat, a pipeline for refining instructions that enables large language models (LLMs) to effectively employ self-composed memos for maintaining consistent long-range open-domain conversations. We demonstrate a long-range open-domain conversation through iterative "memorization-retrieval-response" cycles. This requires us to carefully design tailored tuning instructions for each distinct stage. The instructions are reconstructed from a collection of public datasets to teach the LLMs to memorize and retrieve past dialogues with structured memos, leading to enhanced consistency when participating in future conversations. We invite experts to manually annotate a test set designed to evaluate the consistency of long-range conversations questions. Experiments on three testing scenarios involving both open-source and API-accessible chatbots at scale verify the efficacy of MemoChat, which outperforms strong baselines. Our codes, data and models are available here: this https URL.
(DeepL)我々は、大規模言語モデル(LLM)が一貫した長距離オープンドメイン会話を維持するために、自己合成メモを効果的に使用することを可能にする、命令を洗練するためのパイプラインであるメモチャットを提案する。我々は、「記憶-検索-応答」サイクルの繰り返しによる長距離オープンドメイン会話を実証する。そのためには、各段階に合わせた調整命令を注意深く設計する必要がある。LLMが過去の対話を構造化されたメモで記憶し、検索することを教え、将来の会話に参加する際の一貫性を高める。我々は、長距離会話質問の一貫性を評価するために設計されたテストセットに手動で注釈を付けるよう専門家に依頼する。オープンソースとAPIアクセス可能なチャットボットの両方を含む3つのテストシナリオの実験では、強力なベースラインを上回るMemoChatの有効性が検証されました。私たちのコード、データ、モデルは、こちらのhttps URLから入手できます。

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

