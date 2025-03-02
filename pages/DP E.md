---
title: "DP E"
---

[E - Knapsack 2](https://atcoder.jp/contests/dp/tasks/dp_e)
- 指定された制限重量以下で価値を最大化する[[ナップサック]]問題
- しかし重量を定義域とするDPをするには、制限重量の空間が広すぎる
- [[値域と定義域の交換]]をして、価値を定義域、その価値を達成する最小重量を値とするDPをやる

from [[動的計画法]]
DP_E
- 問題文 [E - Knapsack 2](https://atcoder.jp/contests/dp/tasks/dp_e)

- [[値域と定義域の交換]]
    - 重量の空間が10^11
    - 価値の空間が10^5
    - [[DP_D]]では重量を定義域として価値の関数をつくり、最大値を求めた
    - この問題ではそのアプローチでは定義域が広すぎる
    - そこで逆に価値を定義域として重量の関数を作る
        - そして定義域の中で重量が制約を満たす最大の添字を見つける
    - ![image](https://gyazo.com/8f6820c6fa358d709bd62c806b3166fb/thumb/1000)

python

```
def solve(N, W, WV):
    MAX_VALUE = N * 10 ** 3
    weights = [INF] * (MAX_VALUE + 1)
    weights[0] = 0
    for i in range(N):
        next_weights = weights[:]
        weight, value = WV[i]
        for j in range(MAX_VALUE - value + 1):
            next_weights[j + value] = min(
                weights[j + value],
                weights[j] + weight)
        weights = next_weights
    for i in range(MAX_VALUE, -1, -1):
        if weights[i] <= W:
            return i
```

