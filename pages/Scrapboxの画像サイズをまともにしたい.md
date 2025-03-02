---
title: "Scrapboxの画像サイズをまともにしたい"
---

多分これ「何がまともな状態か」の言語化が必要

まともでない状態
- ![image](https://gyazo.com/f2e0c356b85d2015cc9e60524f8ca747/thumb/1000)
- 2番目の画像がデカすぎる
    - スマホでは画面横幅が小さいのでマトモになる
    - ![image](https://gyazo.com/64dffe659b7e940fe2900d92b76b17f4/thumb/1000)
- 同じ横幅であって欲しいものが縦幅を同一にするために拡大縮小されている
    - ならば`width: 50%`したら？
    - ![image](https://gyazo.com/ea5ea10e60caa05d6209701cb636017f/thumb/1000)
    - `max-height: none !important`
    - ![image](https://gyazo.com/9c70a56101c32b286913b36ee9968310/thumb/1000)

しかしスマホでは小さい
![image](https://gyazo.com/ecbfb89a8e850a923a7bd5038e2510d9/thumb/1000)
- まあそうなるよな…

- max-widthを300pxとかにすれば良いのか？
    - ![image](https://gyazo.com/e16869a50c2dd22a0a1d220ef8ae6d36/thumb/1000)
    - あー、`max-width: 100%`を上書きしたことによってwidthが100%を超えてる時に突き破るのか
    - `width: 100%`
結論
- ユースケースによってはmax-heightではなくmax-widthで揃えたい
