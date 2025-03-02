---
title: "DP W"
---

[W - Intervals](https://atcoder.jp/contests/dp/tasks/dp_w)
- 0と1からなる長さ20万の列があって「この範囲に1があれば何点」というルールが20万個ある、最良の列を作ったら何点になるか求めよ
- 素朴に実装したらどうなるか
    - 2^200000の各数列に対してスコア計算してmax→やばい
    - 各数列について計算する代わりに、途中までの結果を使って効率よく計算できないか？

[EDPC解説 U～Z - kyopro_friends’ diary](https://kyopro-friends.hatenablog.com/entry/2019/01/12/231106)
[[starry sky tree]]
[[遅延セグメント木]]

> `dp[i] = （i まで決めたときに）最後に1にしたのが i であるときのmax。遷移は dp[i] = min(dp[j] | j=0~i-1) 。その後、区間 [l,i] について dp[l~i] に a を足しこむということをやる。segtreeで高速化する（区間addと区間minができれば良い）O((N+M) log N)`
>  なんかこれは自分は典型化できてなかった（ので説明がふわっとしてしまっている）
[https://twishort.com/Vntnc](https://twishort.com/Vntnc)
