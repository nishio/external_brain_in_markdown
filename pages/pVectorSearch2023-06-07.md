---
title: "pVectorSearch2023-06-07"
---

prev [[pVectorSearch2023-06-06]]
- > ネクストアクションはエクスポートを介さずに公開プロジェクトのデータを吸い取ってインデックスにすること

[/halsk](https://scrapbox.io/halsk) 1281 pages
[/yuiseki](https://scrapbox.io/yuiseki) 2679 pages
[/tkgshn](https://scrapbox.io/tkgshn) 5648 pages
まず/halskから
- 127 sec
残り2つ
- 335 sec
done

[[pVectorSearch2023-06-02#647a080aaff09e00006bd34e]]
- [[埋め込みAPI呼び出しの並列化]]
    - [aiohttpとasyncioを使用したPythonの非同期HTTPリクエスト](https://www.twilio.com/ja/blog/asynchronous-http-requests-in-python-with-aiohttp-jp)
    - いまrequestsで叩いてるところをaiohttp.ClientSessionで叩くようにする必要があるのだなー
- "いまrequestsで叩いてる"はFalse
    - openai公式ライブラリを使ってる
    - これはlistで渡してバッチ処理ができる
- [Rate limits : OpenAI API](https://platform.openai.com/docs/guides/rate-limits/overview)
    - 3,500 RPM / 350,000 TPM

並列化をするレイヤーが当初の予定とは違っていた
- embed APIを呼び出す関数かと思ってた
- インデックスを表現するクラスにバッチで実行するメソッドをつけた

できたので走らせて昼食に行く

> This model's maximum context length is 8191 tokens, however you requested 9158 tokens (9158 in your prompt; 0 for the completion). Please reduce your prompt; or completion length.
- oops

PDBで止めて観察
:

```
(Pdb) print(list(map(get_size, texts)))
[85, 122, 88, 118, 5, 106, 100, 100, 9158, 9152, 9164, 121, 113, 81, 456, 133, 45, 6, 6, 7, 514, 351, 278, 441, 322, 27, 210, 515, 517, 252, 23, 28, 363, 92, 486, 318, 350, 326, 276, 340, 418, 355, 309, 292, 366, 334, 273, 387, 349, 341]
```


あー、なるほど、これで1行なのか
- [https://scrapbox.io/yuiseki/https:%2F%2Fplatform.twitter.com%2Fwidgets.js#613321a0bb24d40000440059](https://scrapbox.io/yuiseki/https:%2F%2Fplatform.twitter.com%2Fwidgets.js#613321a0bb24d40000440059)
- チャンクわけしたものが巨大である場合、先頭だけ取ってエンベッドする仕様にする
    - 元々そうしていたが、並列化にした際にエンバグしてたので長いままAPIに投げてしまった

このトラブルのせいでどれくらい時間が掛かるのかわからなくなってしまった
- `238/238 [11:46<00:00,  2.97s/it]`
    - これが修正後に走った[/tkgshn](https://scrapbox.io/tkgshn)のデータ
    - 5748ページあるScrapboxが1万ちょいのチャンクに分けられ、50個ずつ238個のバッチで処理されている
    - 1バッチあたり3秒くらいで、全部で12分という感じ。

Qdrantに入れる
- `ResponseHandlingException: The write operation timed out`
- /nishioの時は`wait=True`なしで叩き込めたんだけど、3人分を一度に入れようとしたら1.5人で死んでしまった
    - WALが溢れたのかな？
    - 追記: インデックス作成との衝突
- `wait=True`をつけたらこんな感じ
    - `117/117 [02:57<00:00,  1.51s/it]`
    - `44/44 [00:54<00:00,  1.23s/it]`
    - まあ数分で入るから気にすることではないか

クロス検索できるようになった
- あれ？なぜかyuisekiばかりヒットするな？？？
- そんなことある？
- あっ `client.recreate_collection` してたw

やり直し
- `wait=True`してても`ResponseHandlingException: The write operation timed out`になるな
- `sleep(1)`しててもなる
- [Bulk upload vectors - Qdrant](https://qdrant.tech/documentation/tutorials/bulk-upload/)
    - あー、なるほど、インデックスの生成を止めるのね
- `23/23 [00:34<00:00,  1.48s/it]`
- `117/117 [02:59<00:00,  1.53s/it]`
- `44/44 [01:15<00:00,  1.72s/it]`
- できた
- [「コンピュータによって熟議や合意形成を支援することに関して」](https://nishio-vecsearch.vercel.app/result/qomP1z9fIIWcaX0YZ4Vp)
    - 横断検索できてる

![image](https://gyazo.com/e23a56be5c403dfdf5d2452e0ec051bf/thumb/1000)
- 余裕だな

今回検証できたこと
- 相手がScrapboxの公開プロジェクトであれば、特に相手の作業は必要ない
- 時間的コストも金銭的コストも大したことない

> [@yuiseki_](https://twitter.com/yuiseki_/status/1666402716841840641): 複数人の個人Scrapboxを結合してベクトル検索できるようにして[[協働]]や[[合意形成]]などにおいて有用か検証しますと言われると、自分のScrapboxに何をどれだけ書くのかという優先度が爆発的に高まるのを感じる

> [@nishio](https://twitter.com/nishio/status/1666413721210740736?s=20): もうしばらくすれば誰でもこれに議題を投げられるようになる
> [/villagepump/Scrapbox ChatGPT Connector座談会モード](https://scrapbox.io/villagepump/Scrapbox ChatGPT Connector座談会モード)

iPhoneで見たら酷いことになってたw
- ![image](https://gyazo.com/fb090d7d77fef80327e2a58e395d05fb/thumb/1000)

> [@yuiseki_](https://twitter.com/yuiseki_/status/1666415420323291141?s=46&t=gkSZtjGEtUZPO0JCzBxCBw): とりあえず重要な情報を100ページくらい追加しました
- update機能を実装せねば...

