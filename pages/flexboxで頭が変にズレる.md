---
title: "flexboxで頭が変にズレる"
---

![image](https://scrapbox.io/files/6ad18cf76bd7d205ec7ead62.jpg)
こういう現象の相談を受けてしばらく悩んだのだが謎が解けたのでまとめ

再現コード
- [https://codepen.io/nishiohirokazu/pen/OJXVBby](https://codepen.io/nishiohirokazu/pen/OJXVBby)
    - ![image](https://gyazo.com/3b12d5d3c011a28e4b22efda00576550/thumb/1000)
- 結論
    - 親divにdisplay: flexがついてない
    - 子divにdisplay: inline-flexがついてる
    - divがインライン要素になったことでベースライン揃えが起きている
- 考察
    - 左右に並べる目的では親divにdisplay: flexがあればいいだけなので子divには必要ない
        - だけども現実のコードはflexで整形した部品を組み合わせて行った結果、元からついていた
    - 親divにdisplay: flexがついてない場合、divはデフォルトでブロック要素なので縦に並んでしまう
    - 子divをdisplay: inline-flexにすると、インライン要素になるので左右に並ぶようになる
        - divの中にコンテンツがなかったりすると一見正しくレイアウトできたように見えてしまう
        - ![image](https://gyazo.com/8535a9689e88fc53afe874c8fbdf5654/thumb/1000)

インライン要素のベースライン揃え
- ![image](https://scrapbox.io/files/6ad18cf86bd7d205ec7ead89.jpg)
- [https://www.google.co.jp/amp/s/html5experts.jp/takazudo/13339/amp/](https://www.google.co.jp/amp/s/html5experts.jp/takazudo/13339/amp/)

[[flexbox]]
