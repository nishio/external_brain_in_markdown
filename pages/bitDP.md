---
title: "bitDP"
---

集合を定義域とする[[動的計画法]]をやる際の実装テクニック。$O(N2^N)$。 N=24で$4\times 10^8$くらい。

ある集合Sについての値を計算する前に、集合Sから要素を一つ取り除いたものについての値が確定して欲しい。
つまり「要素を一つ取り除いたもの」という関係を有向辺とみなしたグラフをトポロジカルソートしてその順に計算したい。
この時、集合の「要素iを含む」と、整数の「i番目のビットが1」を対応づけると、整数の自然な順序がグラフのトポロジカルソートにもなっている。

`mask = 1 << i`として
- $i \in S$: `S & mask`
    - その時の$S / i$: `S ^ mask`

例: [[巡回セールスマン問題]]$m(S,v) = \min_{u \in S} \{ m(S / u, u) + d(u, v) \}$
python

```
def solve_tsp(num_vertex, distance):
    import sys
    INF = sys.maxsize

    SIZE = 2 ** num_vertex
    memo = [[INF] * num_vertex for _i in range(SIZE)]

    memo[0][0] = 0
    for subset in range(1, SIZE):
        for v in range(num_vertex):
            for u in range(num_vertex):
                mask = 1 << u
                if subset & mask:
                    memo[subset][v] = min(
                        memo[subset][v],
                        memo[subset ^ mask][u] + distance[u][v])
    return memo[-1][0]
```

