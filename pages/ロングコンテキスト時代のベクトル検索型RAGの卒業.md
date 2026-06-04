---
title: "ロングコンテキスト時代のベクトル検索型RAGの卒業"
---

2026-03-06
口頭で聞かれて口頭でざっと答えたけど、帰ってきてから念の為ChatGPTに聞いたらいいまとめができたのでメモ
- 余談だけども、こういうまとめは適切に問いを発すればAIがサクッと作ってくれる時代において、この問いを発する力はどうやったら鍛えられるんだろうな

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ロングコンテキストが可能になったLLMにおいてベクトル検索型のRAGよりも良い方法についての議論と論文があると思う、探して報告して
- 最後の要約だけ先に持ってきた
    - <img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>私の要約
        - 「ロングコンテキストLLMにおいて、単純なベクトル検索RAGより良い方法」は確かに複数あり、特に有力なのは
            - 全部入れる
            - 要約ベースにする
            - 階層化する
            - グラフ化する
            - RAGとLCを自動で切り替える
            - チャンク埋め込みを文脈化する
        - です。

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>あります。しかも議論はかなり整理されてきていて、結論は「ロングコンテキスト時代に、単純なベクトル検索RAGが唯一の正解ではない」です。
ただし同時に、「RAGは不要になった」とも言い切れません。いまの主流は、ベクトル検索RAGの置き換えというより、より文脈を保つ検索・圧縮・階層化・ルーティングへの移行です。 ([[Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach]])

ざっくり先に言うと、候補はこの5系統です。
1. LC直投入
    - 小さめの知識ベースなら、そもそも全部入れる。Anthropicは「知識ベースが20万トークン未満なら、RAGなしで全部プロンプトに入れるのが最も単純」と明言しています。 ([Anthropic](https://www.anthropic.com/news/contextual-retrieval))
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これが口頭で「載せられるなら載せたほうがいい」と言ったやつ
2. ハイブリッド・ルーティング
    - 問いによって「RAGにするか、LCにするか」を切り替える。[[Self-Route]] が代表です。LCは平均性能で強いが高コスト、RAGは安いので、両方を使い分ける発想です。
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これは研究的には有用ではあるが、特に社内ユースケースでの実務ではまず「十分な価値を出すことができるか」「それを社内デプロイした時にどの程度アクセスされるのか」が優先して検証されるべきもので、コスト削減はそれらの検証が終わってコストがボトルネックである場合にやることだと思うんだよね。なのでこのアプローチは初手でやるべきではない。
3. 要約・圧縮ベース
    - ベクトルで短いチャンクを拾うのではなく、先に要約や抽出で文脈を圧縮する。2025年の再評価では、summarization-based retrieval が LC に近い性能で、普通の chunk-based retrieval は見劣りすると報告されています。 ([[Long Context vs. RAG for LLMs: An Evaluation and Revisits]])
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これが「コンテキストに載らないならこう言う感じで」と言ったやつ
            - ドキュメント集合が丸ごとコンテキストに載らない時「そのドキュメントがどんな時に参照すべきものなのか」のリストを作ってそれをコンテキストに載せ、LLMにどのドキュメントを参照する必要があるかを考えさせる
4. 階層化・グラフ化
    - 文書やコーパスを、木構造や知識グラフにしてから探索する。
    - これは「局所的な断片検索」では弱い、全体テーマ・関係性・多段推論に強いです。[[RAPTOR]] や [[GraphRAG]] がこの系統です。 ([[RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval]])
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これは個人的には知識ってネットワークになってると思うから興味ある分野ではあるんだけど、実務的には既存のデータからグラフをいい感じに生成できるのか、何か正しくない記述があったらどうやって気づいて修正するのか、というところのエコシステムの発展が追いつく必要があると思う
            - 個人的にはネットワーク上に知識を記述する[[Wiki的システム]]である[[Scrapbox/Cosense]]を使っているわけなんだが、このツールの良さが全然わかってもらえないとも思っているw
5. “ベクトル検索のまま”でも文脈を壊しにくくする改良
    - late chunking や contextual retrieval のように、短チャンク化で失われる周辺文脈を補う方向です。これは「RAGを捨てる」のではなく、「素朴なベクトルRAGを卒業する」路線です。 ([[Late Chunking: Contextual Chunk Embeddings Using Long-Context Embedding Models]])
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これはベクトル研究自体を研究目的で改善したい人は読むといいが、実務的には検索エンジンがそれを実装してきた時にONにするとか、デフォルトでONになるとかのたぐいと思う

重要な背景認識
ロングコンテキストLLMが使えるようになっても、長い文脈を本当にうまく使えるかは別問題です。
有名な Lost in the Middle は、関連情報が入力の真ん中にあると性能が大きく落ちることを示しました。つまり「128Kや1M入る」ことと「長文をちゃんと読む」ことは別です。 ([[Lost in the Middle: How Language Models Use Long Contexts]])
そのため研究の争点は、単なる「RAG vs 長コンテキスト」ではなく、
- 長文をそのまま入れるべきか
- どのように縮約・構造化すべきか
- どの単位で検索すべきか
- 問いに応じて経路分岐すべきか
に移っています。 ([[Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach]])

代表的な論文・手法

1) LC優位だが、RAGと使い分けるべき
[[Retrieval Augmented Generation or Long-Context LLMs? A Comprehensive Study and Hybrid Approach]] (Li et al., 2024, EMNLP Industry)
この論文は、十分な計算資源があるならLCが平均性能でRAGを上回る一方、RAGはコスト面で明確な利点があると報告し、両者を切り替える Self-Route を提案しています。 ([arXiv](https://arxiv.org/abs/2407.16833))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「RAGは劣っているが安い」

2) 再評価すると「要約ベース」が強い
[[Long Context vs. RAG for LLMs: An Evaluation and Revisits]] (Li et al., 2025)
この再検証では、LCがQAで概ね優勢だが、summarization-based retrieval はLCに匹敵し、chunk-based retrieval は劣るとされます。
つまり「単純なベクトル検索RAGが弱い」のであって、「検索を使うこと自体が弱い」わけではない、という整理です。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「単純なベクトル検索RAGはダメ、工夫するとLCに匹敵」→つまりLCできるなら素直にLCしたほうがいい

3) 長い単位で検索する LongRAG
[[LongRAG: Enhancing Retrieval-Augmented Generation with Long-context LLMs]] (Jiang et al., 2024)
短いチャンクではなく、4Kトークン級の長い単位で検索する発想です。
著者たちは、短チャンクだと文脈喪失や hard negative が増えると指摘し、長い retrieval unit と長い reader を組み合わせています。 ([arXiv](https://arxiv.org/abs/2406.15319))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>入れられるコンテキスト幅が小さかった時代のノリで短く刻んでしまってるのはよくないって話

4) 木構造で要約を辿る RAPTOR
[[RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval]] (Sarthi et al., 2024)
文書をチャンク化して終わりではなく、クラスタリング→要約→さらに上位要約という木を作り、必要に応じて複数レベルから取る手法です。
複雑な多段推論QAで改善し、QuALITYで大きな向上を報告しています。 ([arXiv](https://arxiv.org/abs/2401.18059))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これは[[Long Context vs. RAG for LLMs: An Evaluation and Revisits]]の「工夫するとLCに匹敵」の工夫の仕方の一つ
    - 直感的にも納得感がある

5) 全体把握向けの GraphRAG
[[From Local to Global: A GraphRAG Approach to Query-Focused Summarization]] (Edge et al., 2024)
これは特に重要です。著者らは、普通のベクトルRAGはコーパス全体に対する global question、たとえば「この資料群の主要テーマは何か」のような問いに弱いとし、知識グラフ＋コミュニティ要約＋map-reduceで解く枠組みを提案しています。
「全体像を問う質問」では GraphRAG が vector RAG を強く上回ったと報告しています。 ([arXiv](https://arxiv.org/html/2404.16130v2))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これは「塊ごとに要約していく仕組み」の「塊」の定義をどうするかというはなし
    - 十分コストをかけてグラフをメンテしていくなら長期的には良いと思う、研究者なら自分の専門分野の知識をグラフにしてメンテすることに時間を割くのは良い戦略になりうると思う。グラフ的でない新規情報がガンガン入ってくる企業の業務においてどうなのか、一般社員にGraphのメンテを教えるのか、Graphのメンテをできる専門職員が全部署の情報をメンテするのか、AIがGraphをメンテしてくれると期待するのか(まあそのうちできそう)という感じ。

6) チャンクの作り方そのものを変える late chunking
[[Late Chunking: Contextual Chunk Embeddings Using Long-Context Embedding Models]] (Günther et al., 2024/2025)
普通のRAGは「先に切ってから埋め込む」ので前後文脈が消えます。late chunking は、長文全体を一度通してから後でチャンク埋め込みを作るため、周辺文脈を保持しやすい、という提案です。 ([arXiv](https://arxiv.org/abs/2409.04701))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これもまた「塊をどう定義するか」の一種。

7) 実務寄りの Contextual Retrieval
[[Introducing Contextual Retrieval]] (Anthropic, 2024)
論文ではなく技術記事ですが、実務上かなり影響力があります。
各チャンクに「この断片は文書全体の中で何か」という説明文脈を付与する Contextual Embeddings / Contextual BM25 により、失敗検索を大きく減らせると報告しています。加えて、小規模知識ベースなら全部突っ込めとも言っています。 ([Anthropic](https://www.anthropic.com/news/contextual-retrieval))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>実務をやる上ではまずこれは読むべき

8) 圧縮そのものを最適化する xRAG / prompt compression
xRAG: Extreme Context Compression for Retrieval-augmented Generation with One Token (Cheng et al., NeurIPS 2024)
検索結果をそのまま長文テキストとして渡すのでなく、極端に圧縮した表現としてLLMへ橋渡しする方向です。複数タスクで平均10%以上改善、FLOPs 3.53倍削減と報告しています。
Characterizing Prompt Compression Methods for Long Context Inference (Jha et al., 2024)
こちらは比較研究で、extractive compression がしばしば他方式を上回り、最大10倍圧縮でも精度劣化が小さいと報告しています。 ([arXiv](https://arxiv.org/abs/2407.08892))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>どう圧縮するのが良いか、というところが問題。元文書に再利用可能な知識の部分と、人間のコミュニケーションなどに伴う詰め物とがあるわけなので、個人的には検索してから圧縮するより、圧縮(≒要約)してから検索の方がいいのではと思う。

逆に、「LCが常に勝つ」わけでもない
- ここは大事です。
- 特定ドメインでは、RAGの方が long-context full-document 投入より良いという結果もあります。NEPA文書理解の研究では、RAG構成がフルPDF投入より高い正答性を示しました。特に専門文書で、ノイズが多く、必要箇所が局所的なときはRAGが強い、という見方です。 ([arXiv](https://arxiv.org/html/2407.07321v1))

なので現在の合意は、だいたいこうです。
- 小さな知識ベース → 全投入で十分なことが多い。 ([Anthropic](https://www.anthropic.com/news/contextual-retrieval))
- 明示的事実検索 → 改良型RAGが依然強いことが多い。 ([arXiv](https://arxiv.org/html/2407.07321v1))
- 全体テーマ把握・関係性理解・多段推論 → GraphRAG / RAPTOR / 要約階層が有望。 ([arXiv](https://arxiv.org/html/2404.16130v2))
- 計算コストが厳しい → 圧縮やルーティングが重要。 ([arXiv](https://arxiv.org/abs/2407.16833))

いま読むべき論文の優先順位
まず5本ならこれです。
1. Lost in the Middle — 長コンテキストの限界認識の出発点。 ([arXiv](https://arxiv.org/abs/2307.03172))
2. Retrieval Augmented Generation or Long-Context LLMs? — RAG vs LC と Self-Route。 ([arXiv](https://arxiv.org/abs/2407.16833))
3. Long Context vs. RAG for LLMs: An Evaluation and Revisits — 2025時点の再整理。 ([arXiv](https://arxiv.org/abs/2501.01880))
4. RAPTOR — 階層要約型検索。 ([arXiv](https://arxiv.org/abs/2401.18059))
5. GraphRAG — グローバル質問への対抗軸。 ([arXiv](https://arxiv.org/html/2404.16130v2))

私の要約
あなたの問いに一言で答えると、
「ロングコンテキストLLMにおいて、単純なベクトル検索RAGより良い方法」は確かに複数あり、特に有力なのは
- 全部入れる
- 要約ベースにする
- 階層化する
- グラフ化する
- RAGとLCを自動で切り替える
- チャンク埋め込みを文脈化する
です。
