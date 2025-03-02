---
title: "iPad上でのダイレクトタッチとPencilタッチの区別"
---

touchイベントのtouchesで各々のtouchをみると、touchType == "direct" と touchType == "stylus" がある。これで区別する。
[https://stackoverflow.com/questions/34986373/javascript-touch-event-distinguishing-finger-vs-apple-pencil](https://stackoverflow.com/questions/34986373/javascript-touch-event-distinguishing-finger-vs-apple-pencil)

なおChrome開発者ツール上でiPadをエミュレートしてて、マウスでタッチイベントを発生させている時、touchTypeは付いていない。いずれ touchType == "stylus" をエミュレートできるようになるといいな。

将来的には [Pointer Events](https://www.w3.org/TR/pointerevents/) でまとめられるかもしれないが、現時点ではブラウザの実装が進んでいないっぽい。 [[Pointer Events]]

[[iPad]]
