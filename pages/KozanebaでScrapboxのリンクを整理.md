---
title: "KozanebaでScrapboxのリンクを整理"
---

Scrapboxをヘビーに使ってる人(僕)が欲しかった機能が実現できたぞ。
KozanebaにScrapboxのURLを貼るとScrapboxこざねができて、それのexpandメニューを押すと2hop以内のすべてのページがこざねになり、自由に動かせる。

Scrapboxは繰り返し言及する内容のページがあるとだんだんそのページに繋がってるリンクが増えていって、なんだかわけのわからない状態になってしまう。
いくつかのグループに分割するのが好ましいのだが、Scrapbox上ではリンクのカード表示が動かせないのでやりにくい。Kozanebaなら動かせる。

このScrapboxの「KJ法」のページをみると97枚の「KJ法に言及しているページ」がある。言及を繰り返している間にだんだん増えてこうなった。これを整理したい。
![image](https://gyazo.com/eed4b8e9ad08d9dc99b6537b3bbb9a33/thumb/1000)

![image](https://gyazo.com/003e4464393fe4afa658ec9ca544ccc9/thumb/1000)
![image](https://gyazo.com/95a6a78875eb880d322c687e4cca03c6/thumb/1000)
![image](https://gyazo.com/aa2044dcbd24d0a33313a72479e65c51/thumb/1000)
![image](https://gyazo.com/3ba0aafedbc70c3040f790981dee5ed8/thumb/1000)
![image](https://gyazo.com/566102e96a749bde34116f48fb2290f6/thumb/1000)

Scrapboxこざねのタイトルなどをcopy textでコピーしたい、コピーできればそのまま貼りつけて通常こざねを作れる

![image](https://gyazo.com/d43a218fff7b637e7edb47c5fb848774/thumb/1000)
![image](https://gyazo.com/a5fc4d0e1978332aa8d6fd49fd18a4f9/thumb/1000)

選択したグループを画面いっぱいに拡大するメニューが欲しい

一画面以上選択範囲を動かしたい時に、選択してる状態で二本指ジェスチャーでスクロールすると、選択範囲はスクロールしないバグ
選択したままズームアウトしたりしても問題なく動くべき

謎のズレの再現手段として空になったグループをクリックした時に再現しそう

グループごとにスクショ撮ってるのは、全体像はこんな感じで画像で見てもさっぱりだから
![image](https://gyazo.com/2eaee5f71965a88fb8e62aef604b1fee/thumb/1000)

あ、そうか、とりあえずリードオンリー共有をしておくか
[https://kozaneba.netlify.app/#view=mysoGOrUgjEKXjZY4obK](https://kozaneba.netlify.app/#view=mysoGOrUgjEKXjZY4obK)

分類するのは良くないのだけど、分類しなきゃ無理なレベルに散らかってる場合はまずは一旦分類して、小さい空間に分けてから個別にやっつけるのが良いと思うよ

うーん、Scrapboxをもう一歩たどりたいけど、2ホップリンク読み込みすると既存のも含めて大量になるな。
まだないページだけ追加する機能があるといいのかな。

![image](https://gyazo.com/b090bbf68af84fdc4acbeebcccc83529/thumb/1000)
「思考の結節点」系、タイトルだけ見ても置き場所が分からないからと気軽な気持ちで中を開いてしまったが、そもそも「書いた当時の自分が、色々な概念と繋がっていて、切り分けることができず、適切なタイトルを思い付けなかったページ」が「思考の結節点」と呼ばれてるので開いたらヤバかった

まあ、置き場所が定る、って点では「思考の結節点」だけよりは「まあ、ベクトルや次元の話の側だな」となったので進んではいるのだが。
もう26時だし、寝ぼけて変な操作して壊すと怖いからバックアップを作って寝よう

Scrapboxは階層構造を作ることを支援しない
Scrapboxはページ内は箇条書きにより1.5次元で行を動かせるが、それを束ねた物であるページは見た目だけはカード表示だが自由に動かせない

一気に整理する必要はない、何年もかけて蓄積した物だから。1ページから仮に平均10枚のこざねができるとして、1000枚級のかなり大物だ。

明日以降、整理の続きをするよりも、今回使ってみて気になったところを直すことを優先すべきだ。

Scrapboxの良いところは、長年書き溜めたページの中から、人間が手動でつけた特定のキーワードを含むページが手軽に閲覧できること、悪いところはそれが97枚もある時に一覧できなくなること。
Kozanebaの紙の付箋と比較して良いところは、Scrapboxのデジタルデータをそのまま扱えること

1000枚の紙の付箋を作るのは気が遠くなる。デジタルな画像があるのに文字で表現するのもアホっぽいし、画像を印刷したらなら紙をチョキチョキする作業が待っている。物理付箋にこだわるなら付箋プリンターとかが現在の技術の限界だけど、物理にこだわる必要はない。デジタルこざねの方がいい。

デジタルこざねは何百枚広げても物理的な空間を占有しない。片付ける必要がなく、何ヶ月でも色褪せずにとっておける。ノリが剥がれたりしない。Kozanebaにはまだ実装してないけど、デジタルこざねは検索ができる。複製もできるし、重要だと思ったら大きくもできる。詳細な情報へのリンクを持てる。

細かい気になった点
- 範囲選択時の画像のハイライトが変
    - バウンディングボックスがおかしい？
    - 色もおかしい？
- 範囲選択、重い？
    - バウンディングボックスの計算が重い？
    - React更新が重い？
- 二本指スクロール、重い？
    - これもReact更新が重い？
