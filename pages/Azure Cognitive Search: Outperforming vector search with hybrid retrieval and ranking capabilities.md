
![image](https://gyazo.com/8e2fa02e91d9ee1566bd48aeb6008048/thumb/1000)
[https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167)
[[BM25]] + [[Hierarchical Navigable Small World]]([[HNSW]])でのベクトル近傍検索 + [[リランク]]

7/18 パブリックプレビューが開始
- [Azure Cognitive Search にベクトル検索機能が搭載されプライベートプレビューが開始 - Qiita](https://qiita.com/nohanaga/items/f710cac82072b63bc73f)
- [Azure Cognitive Search のベクトル検索を Python で行う](https://zenn.dev/microsoft/articles/34fdf03208b932)

要約
- [[Azure Cognitive Search]]は、従来ベクトル検索を使用していた[[RAG]]アプリケーションの検索ステップを強化する。このプラットフォームは[[ベクトル検索]]をサポートし、関連性を向上させるための追加機能を導入している。この記事では、Azure Cognitive Searchの背後にあるテクノロジーについて、検索とランキングという2つの主要なレイヤーを中心に論じている。特にGenerative AIアプリケーションにおける、セマンティック・ランキングと組み合わせたハイブリッド検索の有効性を強調している。また、ドキュメント・チャンキングの重要性と、セマンティック・ランキングによって最良の結果が優先される方法についても掘り下げている。
- 3つの洞察
    - ハイブリッド検索とセマンティックランキング: Azure Cognitive Searchのハイブリッド検索は、キーワード検索とベクトル検索の両方の方法を組み合わせている。セマンティックランキングと組み合わせることで、特にジェネレーティブAIアプリケーションの関連性が大幅に改善される。
    - ドキュメント・チャンキング戦略： ドキュメントを限られた長さのパッセージにチャンキングすることは、ジェネレーティブAIアプリケーションにとって不可欠である。これにより、文書の最も関連性の高い部分が最初にランク付けされ、文書全体が切り捨てられることなく検索可能であることが保証される。
    - セマンティック・ランキング： Generative AIシナリオでは、上位の結果に優先順位を付けることが重要です。Azure Cognitive Searchのセマンティックランカーは、クロスアテンションメカニズムを備えたトランスフォーマーモデルを使用して較正されたランカースコアを生成し、最良の結果を最前面に表示します。

> [daiki15036604](https://twitter.com/daiki15036604/status/1703913169511727217/history) Azure Cognitive Search のハイブリッド+セマンティックランキングは、純粋なベクターサーチよりもパフォーマンス良かったそうで！
>
>  チューニング不要で今すぐ使用可能！

> [hiro_gamo](https://twitter.com/hiro_gamo/status/1703944092982644958) なんか推しすぎるとうざいかも知れないですが、私の担当してるお客様でも、この「Vector +Keyword SeachにAzure独自のセマンティックリランクを組み合わせた検索」が凄い評判良くて結構移行してくれてて嬉しいんです。Vector単独の類似度って意図したものじゃないときもあるし。

[[検索]]
