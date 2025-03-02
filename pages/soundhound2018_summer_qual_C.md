---
title: "soundhound2018_summer_qual_C"
---

[C - Ordinary Beauty](https://atcoder.jp/contests/soundhound2018-summer-qual/tasks/soundhound2018_summer_qual_c)
- ![image](https://gyazo.com/6027131e902305a403650ddd77ea4749/thumb/1000)
- 考えたこと
    - n^m通りの長さmの数列について、隣り合う2つの差がdである個数の平均値を求める問題
    - m-1の時が求まれば、mの時がわかる
        - m-1の状態と無関係に増分が決まるから
    - 期待値DPかと思ったけど直前の状況に依存しないので単なる掛け算でOK
    - 2個の値があった時に、その差がdである場合の数
        - d=0のときn
        - d<=nのとき2(n-d)
    - 長さmの列にはペアがm-1
        - d=0のとき $(m-1)/n$
        - d<=nのとき$2(m-1)(n-d)/n^2$
- [[公式解説OK]]