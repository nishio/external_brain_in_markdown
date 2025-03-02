---
title: "iPad実機のSafariでプロファイリング"
---

普段はChromeを使っている。実機でのパフォーマンスを調べる必要があったのでiPadのSafariに有線接続した。
「タイムライン」で「収録」するのは、Chromeの「Performance」で「Record」するのと同じ。
どこでサンプリングプロファイラの出力を見ることができるのかわからなくて戸惑った。
「JavaScriptとイベント」を選ぶとChromeの「Event Log」に相当するものが見られる。
![image](https://gyazo.com/093230c3e8d0df713daa1c80c0f2c647/thumb/1000)

コールツリー表示にはここで切り替える
![image](https://gyazo.com/d14381f5f36f6d97fcc74ef809097da6/thumb/1000)

Chromeの「BottomUp」に相当するものはないのかな？

Doc: [https://support.apple.com/ja-jp/guide/safari-developer/dev4fed6a0dc/mac](https://support.apple.com/ja-jp/guide/safari-developer/dev4fed6a0dc/mac)


