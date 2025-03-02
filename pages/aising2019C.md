---
title: "aising2019C"
---

[C - Alternating Path](https://atcoder.jp/contests/aising2019/tasks/aising2019_c)
![image](https://gyazo.com/6eb7e020e386120d4b5fa5a5331e74af/thumb/1000)
- 考えたこと
    - 隣接するマスの色が異なる時、そこは通って良い壁
    - この関係は対称
    - つまり無向グラフの連結成分
    - UnionFindしてから三角数
        - [[頻度→三角数]]の一種
- 公式解説
    - 「黒と白のペア」を見落としてた
        - 任意の2点だと思ってた
        - 三角数ではなく「黒×白」

[[aising2019]]
