---
title: "kozaneba-dev-ai"
---

2026-05-16
[[Kozaneba]]の設計について考える[[KarpathyのLLM Wiki]]

prompt

```
Kozanebaの設計について考えるWiki

筆者nishioは「かんがえをまとめるデジタル文房具Kozaneba」の設計・開発をしている。
間隔をあけて数年にわたって開発が進んできたものなので、記憶が曖昧になってきている。
設計過程での思考のメモなどを集めて構造化していきたい。

raw/nishio.jsonはScrapboxのexport JSONであり、大部分は無関係な内容である。"Kozaneba"というキーワードが含まれているものだけをまず抽出すると良い。

メモを整理・構造化することの最大の目的は、未来により良いものを生み出すことである。
現状のKozanebaの実装を改善すべきか、新しいものを作るべきかは未定である。
そのためにもまずはKozanebaを作り、使うことで得られた知見を収集整理したい。
```


<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>403件ヒット(うち117件はタイトルにKozaneba)。各ページをmarkdownとして抽出し、wiki構造の土台を作ります。
![image](https://gyazo.com/54f9e5c9b7f691fe37026b17b7da953a/thumb/1000)
- そうだ、昔はMovideaって名前だったんだ

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>内 117 ページはタイトルに Kozaneba を含む。期間 2017-09-03 〜 2026-05-16、ピークは 2021〜2023年。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>3つの作業の順番を聞かれたので
- 1: 非日記の概念ページ群(64本)を順に読んで entities/ concepts/ を埋める(Regroup, Movidea, Keichobot, Scrapbox, KJ法, こざね, ねりねり, IOFI, dwell-think, …)
- 2: 日記102本(2021年)を時系列で要約し themes/設計判断ログ.md を作る
- そのあとで
    - 3: 「なぜ作るのか」「Scrapboxとの関係」などについて人間と議論(質問したりする)

> 了解。両方を並行のサブエージェントに任せて、結果を統合して index/log を更新します。まず実ファイル一覧を準備します。
- 1と2を同時にやるのか、まあそれでもいいか

![image](https://gyazo.com/03f5b3f4959169f87ec8a17a7af27c3b/thumb/1000)
どれもグッとこないな
たくさん読んでAIもお疲れなので一旦終わろう
- と思ったのにlintを指示してしまい、それって負担大きい作業だろ感
- 一応lint前にgit commitした
- <img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>追加されたwikiページ(21本)
    - entities 6本: Miro, いどばた, Audrey_Tang, Gendlin, 梅棹忠夫, AIエンジニアたち
    - concepts 15本: 時間的/コンテキスト的スキーム、表札をつけて束ねる、thing、モザイク状の世界、情報の中に住む、なめらかな畳まれ、繰り返しKJ法、クリーンランゲージ、ブロードリスニング、広聴AI、矢印機能、物理演算、チュートリアル、探検ネット勉強会
    - wiki総数: 68ページ(entities 13 + concepts 48 + themes 7)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>改善するか作り直すか
<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>
問い自体を一段ずらして観察を3点だけ置きます。本人にとって既知のものは多いはずなので、ピンと来なければ無視してください。
1. その二項対立は2025-08-29 に nishio 自身が解体している
    - Canvas移行の検討 の最後で「10000件以上をどうするかという路線と、1000件未満の付箋を構造化していく Kozaneba は無闇に同一視しない方が良い」と書いている。つまり「改善 or 作り直し」ではなく「2つの別物として両立させる」が既出の結論候補。問いの形が「単一プロダクトの将来をどう転がすか」のままだと、この自分自身の発見と整合しない。
2. 「作り直し」は既に部分的に走っている
    - canvas-kozaneba-prototype.vercel.app が2025-08-26〜27に動いており、UMAP+格子スナップ+螺旋配置のロジックは「広聴AI のリーフノードを付箋にする」用途として独立した存在感を持つ。判断対象は「するかしないか」ではなく「既存 Kozaneba と canvas プロトの境界線をどこに引くか / 名前を分けるか」。
3. 動機レイヤと技術レイヤは独立に評価できる
    - なぜ作るのか を見ると 2021→2023 で「他人に使われて成長」→「人間の知的能力強化 / Plurality」と動機は変化しているが、揺らいでいない。一方ボトルネック(2000枚のJSONサイズ・1000枚で文字が豆粒)は純粋に技術側。「動機が陳腐化したから作り直す」と「技術が陳腐化したから作り直す」は別の問題で、混ぜると判断が難しい。前者の答えは "No, むしろ強化された"。後者は "Yes, ただし2つに分けて"。

そうだねぇ、動機は変わっていないが技術が陳腐化したかもしれない<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- こざねの形で表現されている断片自体よりも、その関係性を上手く扱いたい
    - 紙の時代には線を引くこと自体が大変だったので断片の側にエフォートが偏ってしまっていた
    - その「紙での作業」を電子化して使ってみる中で「線を引くこと」の重要さがだんだん見えてきてアドホックに機能追加してきた
    - 概念マップを作る実験をしたところで、現状のKozanebaに辺ラベルがないことは問題だと感じるようになった
    - この機能を現状のものの修正としてつけるのか、新しく作るのかを考えているうちに、他にも色々な「過去にこうしたら良いだろうと思ってつけたけど活用されてない機能」が気になってきた
        - たとえば線を引く機能を1:1ではなく「N個の要素の関係」として実装している
            - 1:1に限らない関係の表現ができるべきだと思ったから
            - しかし、大部分のケースで「本当に必要なもの」はそれとは違った
            - 「1:Nで同じ性質の矢印が発生する」とか(目次の章と節の関係など)
            - 一般化しすぎたN項関係のUIはあまり使いやすくない
        - 囲んで畳む機能
            - デジタル画面上ではあんまり
                - 紙の時にはそもそも再配置が高コストであることから、畳むプロセスが1回、開くプロセスが1回で終了だった
                - デジタルで簡単に開閉できるようにしたが「開いてるものを閉じたら隙間があく」という新たな問題が発見された
                    - この隙間を手作業で埋めると、次に開いた時に被ってしまう
                    - グループが開閉されることと、周囲のものとの関係を整合性を持って扱えるビューではなかった
                    - その後「大きな付箋」機能がついて「ズームアウトする」ことをなめらかな畳まれとみなす運用に流れた
                    - しかしそれはそれでごちゃごちゃする、最適ではない

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>つまり「断片に重きを置いた設計」は 紙の物理的制約に由来する歴史的バイアス であり、デジタル化の本来の機会はそこではなく「[[関係性の操作]]」にあったのではないか。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 「関係性の操作」をベースにGPT Proとやりとりしながら散歩してきたんだけど、関係を1対1対象間のエッジとして表現する発想がそもそも問題という気持ちになってきた

<img src='https://scrapbox.io/api/pages/nishio/Karwi/icon' alt='Karwi.icon' height="19.5"/>
- Keichobot/Kozaneba 分業の連続体化: 「言語化 vs 一次元化」の離散分業から、「Situation → Aspect → Relation Field → Projection」のパイプライン上の上流/下流として再配置可能
- この説明は高圧縮すぎて伝わらないと思うが<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - 別途解説させるか
    - [[「Situation → Aspect → Relation Field → Projection」のパイプライン]]


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 改善ではなく全然違うものを作る話になってきたな
- Plan A: [[Keichobot]]の発展形として個人向け言語化支援システムとしてそれを作るのはまあ一つの案
    - 人間とAIの対話が主たる操作方法
        - 選択肢や違和感ボタンや付箋のドラッグは「まだ言語化できていないものをデータ化する手段」という位置付け
- Plan B: いま300件の文章からの知識獲得をしようとしているので、それを支援する機能をつけるのも手
    - Plan Aよりは想定ユーザが多そうだし直近の出口がある
    - 「1万件の可視化」よりは現在の想定データスケールに近いので現在の実装からの修正でカバーできそう
- Plan C: 「Kozaneba読書」にフォーカスするという手もある
    - Plan Aの「あなたの中のまだ言語化されていないものを取り出す」は自分の中に価値のあるものがあると信じられていない人には刺さらない。書籍の中に価値のあるものがあって自分がそれをうまく取り入れられていないと感じている人は多い。

![image](https://gyazo.com/edcfa635737b71109c36de9ac8076666/thumb/1000)

[[吸い取り]]
