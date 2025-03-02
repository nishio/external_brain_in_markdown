---
title: "PAST3O"
---

![image](https://gyazo.com/c243561fb3069ff0f7a2c41046325ef2/thumb/1000)


from [[第三回 アルゴリズム実技検定]]
PAST3O
![image](https://gyazo.com/44f1480ffab9934faa88f95412112586/thumb/1000)
[O - 輪投げ](https://atcoder.jp/contests/past202005-open/tasks/past202005_o)
- 考えたこと
    - [[N個からM個選ぶ]]のを3回やる
- 公式解説
    - [[最小費用流]]
    - 1,2,3回の時のコストの増分が単調増加であることが重要
    - 3本の辺を引くことができる
    - ![image](https://gyazo.com/9e4af4847d4cf7c78354a6753ac9b49c/thumb/1000)
    - ![image](https://gyazo.com/c243561fb3069ff0f7a2c41046325ef2/thumb/1000)

    - 問題を見て最小費用流に帰着するの、何を考えれば良いのか…
        - [[最小費用流に帰着]]作った
- AC
    - グラフの構築
        - 添え字を間違えるミス
        - 負の辺があるとたまに正しくない値を返すのでINFを足しておく
python

```
def solve(N, M, AS, BS, RS):
    INF = 10 ** 5
    mcf = MinCostFlow(N + 5)
    start = N
    goal = N + 1
    round = N + 2
    for i in range(3):
        mcf.add_edge(start, round + i, M, 0)

    for i in range(3):
        for j in range(N):
            r = AS[j] * (BS[j] ** (i + 1)) % RS[i]
            mcf.add_edge(round + i, j, 1, INF - r)

    for j in range(N):
        cs = [AS[j] * (BS[j] ** (k + 1)) for k in range(3)]
        cs.append(0)
        for k in range(3):
            c = cs[k] - cs[k-1]
            mcf.add_edge(j, goal, 1, c)

    return INF * (3 * M) - mcf.flow(start, goal)[-1]
```


