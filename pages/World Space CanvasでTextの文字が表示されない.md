---
title: "World Space CanvasでTextの文字が表示されない"
---

![image](https://gyazo.com/f71a1534a70a00cf0320fe704e30a5e8/thumb/1000)
デフォルトで文字サイスが大きく、かつはみ出した文字が非表示になる設定(Truncate)になってるせい
![image](https://gyazo.com/5feccd9764fb244f24874fadd1446f90/thumb/1000)
TextのScaleを0.05ぐらいにするとだいぶ期待に近い見栄えになる
![image](https://gyazo.com/7bc763265ad87473d96715868ba61519/thumb/1000)

デフォルトのWrap, TruncateではなくOverflowにしておいた方が不慣れなうちは失敗したときの挙動がわかりやすくてよいのではないか。
![image](https://gyazo.com/8cb4cf8daed4aab2f7dfaf41affa1411/thumb/1000)
[[リッチテキストのマークアップはHTMLではない]]

[[World Space Canvas]]
[[Text]]
