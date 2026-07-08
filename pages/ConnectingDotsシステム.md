---
title: "ConnectingDotsシステム"
---

関連
- [[Connecting Dots]]
- [[自己紹介と歴史は共通の構造を持つ]]

ストーリーは主観的
- [[事実に基づいたストーリーテリング]]
    - 歴史的事実に基づいていても解釈が混じる
    - なにが事実で何が解釈か明瞭に分離したい
- 事実の集合は人間が読むには向かない
    - ただしAIが読む場合には事実と解釈の明瞭分離されたドキュメントとして有益
- 事実の間の関係性はたくさんありすぎて一次元の文章で表現困難
    - ストーリーを作る上ではそれが取捨選択されている
    - 何を「重要」とみなして選択するか、何を捨てるかに人間の価値判断が混じっている

[[事実の島の周りに解釈が広がっている]]

2026-04-26
- 設計を考える[[KarpathyのLLM Wiki]]を作った `connecting-dots-design`
- <img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>ConnectingDotsシステムの設計に関する西尾さんの既存思考(Cosense 2hopダンプ、計18ページ、約1280行)を把握しました。
    - 要旨を一言で言うと: 「点(Dots:検証可能な事実)・線(Stories:キュレーション)・面(Views:表示)」の3層で、自己紹介とPluralityの歴史を同じ仕組みで扱う設計。
- <img src='https://scrapbox.io/api/pages/nishio/KarpathyのLLM Wiki/icon' alt='KarpathyのLLM Wiki.icon' height="19.5"/>「[[自己紹介ポーカー]]」が Story の本質を最も簡潔に言語化していた
    - [[自己紹介とポーカーの役]]

2026-07-08
- ConnectingDotsシステムと[[Kozaneba]]の融合
    - Dotsはこざねである
    - [[こざね法]]における「こざねをあつめてホッチキスで止めたもの」がDotを配列したものである
    - 多くの場合、それの配列を直接読者に見せるのではなく、グルーや補足説明が必要
