---
title: "DP A"
---

[A - Frog 1](https://atcoder.jp/contests/dp/tasks/dp_a)
- スタートからゴールへ行く
- 各点で1つ進むか2つ進むかの2通りの選択肢があり、それによってコストが異なる
- ゴールに至る最小コストを求める問題
- 各点を定義域とし、そこに至る最小コストを値とするDP

from [[動的計画法]]
DP_A
とりあえずなんとなく書いてみたら、[[集めるDP]]だった
python

```
def solve(N, heights):
    costs = [0] * N
    costs[0] = 0
    costs[1] = abs(heights[1] - heights[0])
    for i in range(2, N):
        costs[i] = min(
            costs[i - 2] + abs(heights[i] - heights[i - 2]),
            costs[i - 1] + abs(heights[i] - heights[i - 1]),
        )
    return costs[-1]
```


これをあえて[[配るDP]]で書いてみた
- 「今入ってる値と、新しい値の小さい方を選ぶ」という書き方のため、十分大きな値INFで初期化している
- 実はこの問題に関しては2つ目のminで常に新しい値が小さいし、必ず最初に更新されるので、ここをminでなくして、コストを初期化しなくしてもよい
- iがゴールの直前まで走る必要があるのに、2つ先まで参照するので、範囲外アクセスを避けるために一つ大きく確保する必要があった
    - これに相当することは集めるDPでは「0と1を事前に計算」「ループを2から始める」という形で対処している
- 個人的には、ちょっと頭をひねる必要がある感じ
python

```
def solve(N, heights):
    heights += [INF]
    costs = [INF] * (N + 1)
    costs[0] = 0
    for i in range(N - 1):
        costs[i + 1] = min(
            costs[i + 1],
            costs[i] + abs(heights[i + 1] - heights[i]))
        costs[i + 2] = min(
            costs[i + 2],
            costs[i] + abs(heights[i + 2] - heights[i]))
    return costs[N - 1]
```


[[メモ化再帰]]で書いたもの
- これは素直
- どの値が計算済みかはメモ化の部分に押しつけて、人間は気にしていない
- 計算済みかどうかを識別できる必要があるので、コストとしてあり得ない値(None)で初期化してある
python

```
def solve(N, heights):
    costs = [None] * N
    costs[0] = 0
    costs[1] = abs(heights[1] - heights[0])

    def get_cost(i):
        if costs[i] != None:
            return costs[i]

        c = min(
            get_cost(i - 2) + abs(heights[i] - heights[i - 2]),
            get_cost(i - 1) + abs(heights[i] - heights[i - 1]),
        )
        costs[i] = c
        return c

    return get_cost(N - 1)
```

