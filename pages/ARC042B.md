---
title: "ARC042B"
---

[B - アリの高橋くん](https://atcoder.jp/contests/arc042/tasks/arc042_b)
- ![image](https://gyazo.com/263d6aa4a32eefc4ab4ee0a3987ad48f/thumb/1000)
- 考えたこと
    - 点と線分の距離
    - 垂線の足が線分の中にあればそこまでの距離、なければ端点のどちらかへの距離
    - 凸多角形の条件から今回は端点は有り得ない
    - PからABへの垂線の足は、APからABの方向成分を取り除けば求まる
- 公式解説
    - 僕はベクトルで解いたけど公式解説は複素平面で解いてた

[[ARC042]]
