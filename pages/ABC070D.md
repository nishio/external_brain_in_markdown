---
title: "ABC070D"
---

[D - Transit Tree Path](https://atcoder.jp/contests/abc070/tasks/abc070_d)
- ![image](https://gyazo.com/7747dc17e290d49629796ab6d7387f3a/thumb/1000)

- 考えたこと
    - Kは全体で一つ
    - つまりKからすべての頂点への距離を前計算しておけば、クエリでは2つのパスの長さを足し算するだけ
    - Kを始点としてDFSして各頂点の距離を決めればよい
- 公式解説
    - 方針は同じ
    - [[閉路がない連結グラフの二頂点間のパスは一通り]]
    - 隣接行列でグラフを持つとMLE
        - 普段そんな持ち方してないのでハマらないけど
