---
title: "AGPLパズル"
---

某所でライセンスの議論をしてて、実際の出来事と違うんだけど、少しひねると面白い状況設定の出題ができそうだと気づいた(そして僕は不正解だった)

状況設定
- Aさんは期間限定のWebサービスを提供し、終了後にソースコードを公開するつもりである。
- t1時点でAGPLのライブラリXを使ってWebサービスver.1を提供した。
- その後MITライセンスのライブラリYでXと同様の目的が達成できることに気づき、
- t2時点でライブラリYを使ったWebサービスver.2でリプレースした。
- 現在、サービス提供終了後の時点t3である。ソースコードを公開しようとしている。この時AGPLでの公開が要求されるか？

Bさん:
- そもそもt1の時点でAGPLで公開する必要があったのでは？
Cさん:
- いや、ユーザからのソースコード提供リクエストがあった後で提供すれば十分ライセンスの条件を満たす。
- だから、ver.1に関してはソースコード提供リクエストがないままサービス終了してのでOKだ。
- そしてver.2に関してはAGPLのライセンスを使っていないので今後の公開でAGPLにする必要はないだろう。
Bさん:
- サービス終了後のt3現在でもver.1のコードは公開しつづける必要がある。

問い
- どちらの意見が正しいか、もしくはどちらも正しくないか、理由をつけて説明せよ
