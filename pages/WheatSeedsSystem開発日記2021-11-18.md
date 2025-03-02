---
title: "WheatSeedsSystem開発日記2021-11-18"
---

[[pWheatSeedsSystem]]
[[複数のリソースパックを組み合わせる仕組み]]
![image](https://gyazo.com/5a4c77e9fc384b151da1140a3c0d5483/thumb/1000)
- 元々、[[CybozuHackathon2021]]でサーバリソースパックとして使ったのですべてのものが一つのリソースパックに入っていた(1)
- ハッカソン後にリソースパックをリリースするにあたって「色々入ったリソースパックです」ではタイトルとかつけにくい
    - 「サイボウズハッカソンで作ったやつ」ってタイトルは微妙なので
    - というわけでテーマごとに分割してリリースした(2)
- ところがこの設計だとseed部分は同一のオブジェクトなので複数のリソースパックを導入すると後のものが先のものを上書きして動かなくなってしまう
    - そこですべてのパックのseedにすべてのオブジェクトへの参照を入れる(3)
- これでも動かないので同一パック内のオブジェクトしか参照できないのかと焦った
    - 元々作る予定だった全部入りパックを作ってみたが問題は再現したのでパックを跨いで参照できないことが原因ではなかった
    - 原因はこれ
        - [https://github.com/nishio/wheat_seeds_system/commit/98b1dca242f0ede0129a0e6001811dff1a5b0279](https://github.com/nishio/wheat_seeds_system/commit/98b1dca242f0ede0129a0e6001811dff1a5b0279)

リリースした
> I released v0.5.0 and now you can use this pack with other wheat system packs!

レベルが10になった
