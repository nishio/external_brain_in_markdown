---
title: "Promiseの歴史"
---

[The history of Promises](https://samsaccone.com/posts/history-of-promises.html)
- この人が十分すぎる充実度の解説を書いていた。下記は僕の要約と加筆。

Promiseのアイデアの源流は古い
- [Future パターン - Wikipedia](https://ja.wikipedia.org/wiki/Future_パターン)
- [Futures and promises - Wikipedia](https://en.wikipedia.org/wiki/Futures_and_promises)

1997年のE言語がほぼ今のPromiseと同じ形のものを作っている
- [E (programming language) - Wikipedia](https://en.wikipedia.org/wiki/E_(programming_language))
2001年にPythonで実装されたネットワークプログラミングフレームワークのTwistedがE言語を参考にして実装された
- Deferredと呼ばれていた
- [Twisted - Wikipedia](https://ja.wikipedia.org/wiki/Twisted)

2005年にJavaScriptの軽量ライブラリMochiKitがTwistedを参考にして実装された
- 当時[XMLHttpRequest - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)が使われていた、今のfetchに慣れた人からするとすごくめんどくさい<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - これを楽にしたいという意図があった
- [MochiKit - Wikipedia](https://en.wikipedia.org/wiki/MochiKit)

Dojo、QなどいくつものJavaScriptライブラリが同様の概念を採用し始める、そして2010年にjQueryが採用する
- [Dojo Toolkit - Wikipedia](https://ja.wikipedia.org/wiki/Dojo_Toolkit)
- [Q](https://github.com/kriskowal/q)
- jQueryは少なくとも一時期はとてもメジャーなJavaScriptライブラリだった<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - あまり詳しくない人がとりあえず入れて使う的な空気感
    - jQueryによって「こういうやり方」が広い範囲のJavaScriptプログラマに広がることになった

統一的なテストケース[Promises/A+](https://promisesaplus.com/)が生まれ、まちまちだった「こういうやり方」の実装が「同じ振る舞いをするPromiseの実装」となった
- また、このことにより「Promise」という一つの概念が広い範囲で使われていることを客観的に示すことができるようになり、標準化の助けになった

そして2015年に[[ES2015]]という形で標準化された。

[[コーディングを支える技術加筆案]]
