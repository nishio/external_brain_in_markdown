---
title: "flexboxで頭が変にズレる"
---

![image](https://gyazo.com/8b4090e732de5400efd7e902063fa21a/thumb/1000)
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
- ![image](https://gyazo.com/de07862ebf5706f4860cd1454ad705f9/thumb/1000)
- [https://www.google.co.jp/amp/s/html5experts.jp/takazudo/13339/amp/](https://www.google.co.jp/amp/s/html5experts.jp/takazudo/13339/amp/)

[[flexbox]]
