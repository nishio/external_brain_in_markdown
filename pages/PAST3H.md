---
title: "PAST3H"
---

from [[第三回 アルゴリズム実技検定]]
PAST3H

H ハードルが置かれたコースを飛んだり飛ばなかったりして走る時の最短時間を求める。
地点xに至る最短時間を小さいxから順に求める。[[動的計画法]]

python

```
if 1:
    N, L = [int(x) for x in input().split()]
    XS = [int(x) for x in input().split()]
    T1, T2, T3 = [int(x) for x in input().split()]
if 0:
    if 1:
        L = 10
        XS = []
        T1, T2, T3 = 2, 2, 2
    if 1:
        L = 10
        XS = []
        T1, T2, T3 = 2, 4, 2
    if 1:
        L = 10
        XS = []
        T1, T2, T3 = 4, 2, 2
    if 1:
        L = 10
        XS = [5]
        T1, T2, T3 = 2, 4, 4

isHurdle = [False] * L
for x in XS:
    isHurdle[x] = True

answer = 1e+99
# print(isHurdle)


def minUpdate(p, t):
    # print("update?", p, t)
    if p > L:
        t = time + T1 // 2 + int((L - position - 0.5) * T2) + penalty
        p = L

    if fastestTimes[p] > t:
        fastestTimes[p] = t
        # print("updated")


fastestTimes = [1e+99] * (L + 1)
fastestTimes[0] = 0


for position in range(L):
    time = fastestTimes[position]
    penalty = T3 if isHurdle[position] else 0
    minUpdate(position + 1, time + T1 + penalty)
    minUpdate(position + 2, time + T1 + T2 + penalty)
    minUpdate(position + 4, time + T1 + 3 * T2 + penalty)
    # print(fastestTimes)

print(fastestTimes[L])
```

