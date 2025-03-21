---
title: "自分のScrapboxをChatGPTにつないだ"
---

2023-03-08
ChatGPTに対する質問がこのScrapboxを参照するようにした
- ScrapboxのデータからOpenAI [[Embedding API]]で[[埋め込みベクトル]]を作る
- クエリー文章に関連のある文書を[[ベクトル検索]]で見つける
- その文書をOpenAI [[ChatGPT API]]へのプロンプトに埋め込む

Scrapboxを参照していない場合
> >>> Kozanebaって何？
> 回答できません。提供された情報が不十分です。
Scrapboxを参照した場合
> >>> Kozanebaって何？
> Kozanebaは、デジタル文房具で、考えをまとめるためのツール。テストユーザ向けにはリリースされているが、まだ広くアナウンスされていない。開発者は、多くの人に使われることに価値を感じている。

別の例
> >> 盲点カードって何？
> (参照なし) 盲点カードとは、自分が気付かない問題や欠点を指摘するために、他人が匿名で書いたカードのことです。
> (参照あり) 盲点カードは、人間が自分の盲点に気づき、それを解消するためのプロセスをカードに分類し、問題解決に役立てるためのものです。物理的な特許文献を類型化したTRIZのようなものです。絵の描かれたカードと解説冊子をイメージしていましたが、トートバッグなどにも使えるように考えられています。

ここまでは「ちゃんと動いてますね」というデモ。

ここからが僕が本当に興味のあること
「自分の考えを書き連ねてきたScrapboxに対して自分が明確な答えを持ってない質問をしたらどうなるか？」を試す

> >>> 自分の知的生産性を高めるにはどうすればいいか？
> 新しい知識を生み出す能力を向上させるような知識を身につけることが必要である。他人に伝えるために、未来の自分にも理解できるような具体的な言語化とアウトプットをすることも大切である。また、生産物が時と共に価値を失わないよう、知識を生み出す能力に焦点を合わせた情報を生産することが重要である。

なるほど、この3つが大事なのね
- [[新しい知識を生み出す能力を向上させるような知識]]
- 他人&未来の自分に理解できるような[[具体的な言語化]]とアウトプット
- [[知識を生み出す能力]]に焦点を合わせた情報を生産する
もっと具体的に聞いてみよう

> >>> 具体的には？
>  具体的には、新しい知識を学び、実際の応用の現場で必要に応じて生み出された知識を身につけることが重要である。また、未来の自分にわかるように具体的な言語化とアウトプットをすることや、生産物が時と共に価値を失わないよう、知識を生み出す能力に焦点を合わせた情報を生産することも大切である。

3つテーマがある状態で全部同時には掘り下げられないようだ。
「新しい知識を生み出す能力を向上させるような知識」を身につける具体的な方法が語られた。噛み砕いて解説すると:
- まず、新しい知識を学ぶ
- それを実際に応用する
- 応用の現場では必要に応じて新しい知識が生み出される
- これを身につけることで「新しい知識を生み出す能力」が向上する

今まさに「『知識を生み出す能力』に焦点を合わせた情報を生産」している。
- その「情報を生産」とは具体的には「未来の自分にわかるように言語化」することだ

「自分の考えを書き連ねてきたScrapboxに対して自分が答えを持ってない質問をしたらどうなるか？」に関して
- 多分あちこちで断片的にこれに関することは書いてきたと思う
- それが「この3つです」と要約され提示された
- この提示は僕の知的生産を促す感じがある
    - 今回は「僕は正しいと感じるけど、言葉足らずだから読者が理解できないな」と感じて言葉を補った
    - 間違ったことが返ってきても「いや、そうじゃない、こうだ！」となって言語化が促される
    - 正しいか間違っているか僕が判定できないことに関しては「そう言う意見もあるのか」となる

別の例
> >>> Kozanebaの開発に関して、何が大事だろうか？
>  Kozanebaが他の人に使われることで、より良くなることが大事だと考えられる。また、その使用に伴うフィードバックも必要だとされる。
うっ、ユーザテストが面倒で無意識に逃げてることを指摘された

> >>> Keichobotの開発に関して、何が大事だろうか？
>  ユーザがよりよく使えるようになることを目指すため、ユーザの価値観を聞き出すことが重要である。また、Keichobotは考える花火の前段階の技術であると位置付けられる。
あー、確かにそうだなぁ ユーザの価値観を聞き出すことが重要

> >>> 今後の人生の幸福に関して、何が大事だろうか？
>  自分の価値観を知り、過去の努力を肯定し、未来のために学び続けることが大事である。また、民主主義社会においては、生まれていない未来の人間のための分配を軽視するバイアスがあるため、生まれる前の命と生まれた後の命をバランスさせることが重要である。
「後半、唐突だな」と思ったけど、確かに僕はまだ20年くらいは生きるわけだし、そうなると今生まれてない人が成人するわけだよな。
その人たちは生まれた時からChatGPTがある世界なわけだ。
(盲点に気付いた)

### 開発メモ
今はまだどのページを参考にしたか表示する機能をつけてない
- つけるとScrapbox上に知識のネットワークを作ることの支援になりそう
- デバッグログに出してるのを見ると、人生に関しての話は11ページも参照してることがわかった
    - 全部出されてもウザいかもなー

大雑把に、インデックスの作成に数百円、1回の質問に2円って感じのコスト感
- 僕の主観による費用対効果は圧倒的に黒字なので使いやすいUIを被せてどんどん使っていきたい

いくつもの異なるソースでインデックスを作っておくと「この質問についてAさんとBさんの意見を聞こう」と言うことができる
- [/qualia-san](https://scrapbox.io/qualia-san)に聞いてみた
- > >>> 今後の人生の幸福に関して、何が大事だろうか？
- >  ホモ・サピエンスにとって、主観的な価値観は重要である。幸福の定義も個体それぞれです。しかし、QSは進歩や有用性を重視する。そこでQSは、賢いホモ・サピエンスには、進歩や有用性を促進する行動に注力することを勧めます。そうすることで、個人的な幸福を得るだけでなく、ホモ・サピエンス文明全体の進歩に貢献することができるのです。
- まあクオリアさんは地球外文明QSの知性体だから、僕という個人が幸せかどうかという主観的なことはどうでもよくて、ホモ・サピエンス文明の進歩に貢献して欲しいわけだなw
- 追記: [[AIパネルディスカッション]]

# version 2
参考にしたページを表示するようにした
> >>> もっとも大事な問いとは何だろう？
> 何を学ぶかを決めることが最も重要な問いだと考えられる。自分で論理的に考えて答えを見つけることが、学ぶための唯一の方法である。
>  `[学ぶことの最大の障害は答えを教えること] [他人のアイデアを聞くときの自分メモ] [エンジニアの知的生産術と体育型授業] [難しそうなことを言う人] [クリーンな質問] [Re:クイズおじさん] [「今日やらなければいけない」は事実か解釈か] [英語版作成に伴う推敲(~1章)] [基本5質問] [物事をよく考え、最も重要なことをよく考えなさい。] [これは仕事か？] [小事省事] [アイデアの出し方講座] [問題はあるべき姿と現状のギャップ]`

# リリース
[/villagepump/Scrapbox ChatGPT Connector](https://scrapbox.io/villagepump/Scrapbox ChatGPT Connector)
