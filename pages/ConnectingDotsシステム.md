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

2026-07-29
- [[grasp]]によってあちこちの情報を一括して参照できるようになったことと、Opus5が来たことと、次の週末に[[デジタル民主主義サミット2026]]があるので登壇者情報を出さないといけないという[[アウトプットのニーズ]]によって[[2026自己紹介ページを更新した]]
    - [[適切な切り出し方は、ニーズが明らかになった後に決まる]]
        - 十分な情報が集まった場所(今回はLLM Wikiがgraspで結合されたもの)があれば、自己紹介用のWebページを作るという作業は「[[切り出し]]」の一種

「ConnectingDotsシステム」に関する考察は深まったが、現時点での結論は「これに特化したシステムを作る必要はない」
- Opus5はこのシステムの設計議論を読んだ上で「LLM Wikiからgraspで情報(=dots)を集めて、そのdotsを並べたstoryのHTMLページを生成」まで一気にやった

- Dotsの中には「私に帰属しないもの」がある
    - 国連IGF京都の話が書かれていて何かなと思ったらAudreyがTalk to the Cityを紹介した出来事だった、それは私がやったわけではない
    - 「私に関係ない」かどうかはまた別の話
        - [[因果関係はあるが、私が因ではない]]、という感じか
    - > IGF京都2023（インターネット・ガバナンス・フォーラム京都2023、2023年10月、総務省開催の国連関連会議）は、Audrey Tang が講演でTalk to the Cityを紹介した場であって、西尾さんが可視化を実践した事例ではありませんでした。Scrapboxの元記述も「Audrey TangがTalk to the Cityを紹介した」で、西尾さん自身の関与を示すものではありません。私がストーリーに practice の一例として並べたのは過剰な帰属で誤りだったので、削除しました。
- 帰属が明確ならStoryに混ざってても良い
    - むしろ「自分起因のDotsしかStoryに含めない」とやると、後からStoryを読む人が理解しにくいものになってしまう

2026-07-30
- 自己紹介ページの更新の過程でDotsとそれをつなげたStoryを作るという行動に関して5件の実例ができた
    - [ブロードリスニングの実践 — 西尾泰和](https://nhiro.org/broadlistening/ja.html)
    - [Plurality — 西尾泰和](https://nhiro.org/plurality/ja.html)
    - [人材育成 — 西尾泰和](https://nhiro.org/mentoring/ja.html)
    - [知的生産 — 西尾泰和](https://nhiro.org/intellectual-production/ja.html)
    - [高次元ベクトルの可視化 — 西尾泰和](https://nhiro.org/highdim/ja.html)
- やっている間に西尾から突っ込まれた経験から「[[全Dotが真でも繋ぎ目が偽ならStoryは偽]]」という言語化がされた
    - 事実であるDotを集めて「事実の集合」を作るところまでは問題ない
    - それを繋いだStoryを作る段階で「事実でないもの」が含まれる可能性がある
        - AIが想像で間を埋めるのでハルシネーションの可能性がある
        - またこれはKJ法的に言えば「集めた付箋がなぜ集まっているのかをストーリーにすることで創発が行われる」という捉え方もできる
        - どちらにせよ、そこで生成されたものの人間によるレビューが必要
- 自己紹介ページに載せるほどでもないけどStory(=[[系譜]])として出力されたもの
    - [[考えを整理するツールの系譜]]

2026-07-30
- [[何がDotsであるか]]

2026-07-31
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>現時点で「トップからリンクしてるストーリーに含まれるドット」でないとしても、将来振り返ったときにつながる可能性があるドットに関して、AIのクロールや検索で発見可能な対象として整備されているべき
- <img src='https://scrapbox.io/api/pages/nishio/Opus5/icon' alt='Opus5.icon' height="19.5"/>
    - dots.json  # ★AIクロールの一次面: 全Dotのマニフェスト（全フィールド+status+verifiability）
        - LLM は数百〜数千 Dot なら manifest を読んで推論・grep で足りる。主オーディエンス（未来の後ろ向き接続者＝AI）にはこれが本命。まずこれだけで要件を満たす。
    - sitemap.xml  # 全Dot URLを列挙 → クローラが漏れなく辿れる
    - llms.txt  # 「Dotの一次データは /dots.json」をAIに明示（クロール誘導の作法）
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>なるほどね〜
    - この後、Webサイトの自己紹介でStoryを生成した時に使われたDotsを抽出してみる
    - 当初「Dotsを作る、それを並べてStoryを作る」と考えていた
        - 暗黙に「人間がそれを並べてStoryを作る」だった
        - AIが膨大なデータからDotsの抽出とStory作成までを一気にやったのが今回の自己紹介update

- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>旧プロトタイプにある自己紹介 Dot と今回自己紹介作成にあたってStory生成した結果としてpick upされたDotsとの間にどのような差があるか検討したい
    - <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>
        - Set A（旧プロトタイプの profile Dot）＝約15件。「最近の活動＋基本経歴」をマイルストーン単位で上から選んだもの（born / 博士 / 入社 / 著書 / 学位 / 理事就任 / 近年のブロードリスニング活動）。
        - Set B（今回の5 facet Story の Dot）＝約40件（重複除く）。テーマの縦糸を辿った結果、中間・連結の Dot まで湧き出したもの。
        - つまり A は「プロフィール枠を先に決めて代表イベントを摘む」トップダウン、B は「縦糸を辿って必要な点を掘り出す」ボトムアップ。これが一番効いている差です。縦糸を通すには支える点が要るので、Story 生成そのものが Dot 発見装置になっている（「[[線を引く行為が点を発見させる]]」の実証）。
    - 深い差：同じ出来事が Story の高度で別 Dot になる
        - 24歳博士（2006）：A では「博士取得」という経歴マイルストーン Dot。B（highdim）では「球面SOM で高次元遺伝子発現を可視化する研究」＝ベクトル可視化の縦糸の起点として再枠付け。同じ時期でも Story の角度が違えば別 Dot。
        - word2vec本（2014）：A＝著書 Dot、B-intellectual-production＝著書、B-highdim＝「単語を高次元ベクトルで表現」。1出来事が3つの枠で現れる。
        - 未踏理事（2015）：A＝就任 Dot、B-mentoring＝2015–2025 の期間 Dot（退任込み）。
    - 24歳博士のように「A ではマイルストーン、B では研究の起点」と枠がかなり違う場合、本当に1 Dot＋2 caption で足りるか、それとも event 文言が枠に引きずられて事実部分を切り出しにくいか。
        - word2vec本（2014）→ 畳める
        - 未踏理事（2015–2025）→ 畳める
        - 24歳博士（2006）→ 畳めない
            - 畳もうとすると event を「博士取得（credential）」にするか「球面SOM研究（research）」にするか選ばされる
            - さらに mentoring 用の「NAIST で後輩に教える立場に」も同期間の第3の事実。博士期は最低3つの sub-fact の container
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>未踏の理事も「理事をやっていた期間」と「未踏ジュニアの設立」と「未踏ジュニアのメンター(継続中)」は別factじゃない？
            - <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>私が間違えた根因は、元の facet Story の <li> 項目「2016年– 未踏ジュニア コファウンダー・メンター」自体が2つの fact を束ねていたこと。
        - <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>mentoring「ITスクール2004・2005／ICTスクール2006 チューター」＝3回のチューター
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>分けて語るエピソードがないからまとめといていいんじゃないかな

