
from [[動的計画法]]
DP_B
まずは[[配るDP]]
python

```
def solve(N, K, heights):
    heights += [INF] * K
    costs = [INF] * (N + K)
    costs[0] = 0
    for i in range(N - 1):
        for k in range(1, K + 1):
            costs[i + k] = min(
                costs[i + k],
                costs[i] + abs(heights[i + k] - heights[i]))
    return costs[N - 1]
```


ところが3TLE
下記のように関数呼び出しを削ったが1TLE残った
Numbaでコンパイルしようかと思ったが
PyPyで提出、165msec AC

python

```
def solve(N, K, heights):
    heights += [INF] * K
    costs = [INF] * (N + K)
    costs[0] = 0
    for i in range(N - 1):
        for k in range(1, K + 1):
            newcost = costs[i] + abs(heights[i + k] - heights[i])
            if newcost < costs[i + k]:
                costs[i + k] = newcost
    return costs[N - 1]
```


[[集めるDP]]、
- 1625 ms AC
- PyPy 385 ms
python

```
def solve(N, K, heights):
    costs = [0] * N
    costs[0] = 0
    for i in range(1, N):
        costs[i] = min(
            costs[j] + abs(heights[i] - heights[j])
            for j in range(max(i - K, 0), i)
        )
```


- 8TLE
- PyPy 540 ms AC
python

```
def solve(N, K, heights):
    costs = [None] * N
    costs[0] = 0

    def get_cost(i):
        if costs[i] != None:
            return costs[i]

        c = min(
            get_cost(j) + abs(heights[i] - heights[j])
            for j in range(max(i - K, 0), i)
        )
        costs[i] = c
        return c

    return get_cost(N - 1)
```

