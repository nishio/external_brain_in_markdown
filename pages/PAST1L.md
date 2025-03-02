
[L - グラデーション](https://atcoder.jp/contests/past201912-open/tasks/past201912_l)
![image](https://gyazo.com/622d3e70835a1497220daa46d7958222/thumb/1000)
- 考えたこと
    - 30個の頂点を最短コストでつなぐ
    - 5個の補助的な頂点があって、それは繋いでも繋がなくても良い
    - 厄介だな
    - 2^5の「5個の頂点を選ぶかどうか」に関して最小全域木を求める？
        - 頂点を取り除いてコストが改善することはないので大きい方からやってもいいかもだけど、それをやるまでもなく間に合いそう
- 公式解説
    - [[シュタイナー木]]問題
        - しかしT=30なので [[Dreyfus-Wagner]] O(n 3^t + n^2 2^t + n^3) では間に合わない
    - [[最小全域木]]
        - [[クラスカル法]] O(E log E)
    - 35頂点で辺は10^3ぐらいなので2^5の全パターンで探索しても余裕で間に合う
- 1WA
python

```
def solve(N, M, LARGE, SMALL):
    from math import sqrt
    edges = []
    for i in range(N):
        x1, y1, c1 = LARGE[i]
        for j in range(i + 1, N):
            x2, y2, c2 = LARGE[j]
            d = sqrt((x1 - x2) ** 2 + (y1 - y2) ** 2)
            if c1 != c2:
                d *= 10
            edges.append((d, i, j))
    large_edges = edges[:]

    INF = 9223372036854775807
    ret = INF
    for subset in range(2 ** M):
        edges = large_edges[:]
        for m in range(M):
            if subset & (1 << m):
                x2, y2, c2 = SMALL[m]
                for i in range(N):
                    x1, y1, c1 = LARGE[i]
                    d = sqrt((x1 - x2) ** 2 + (y1 - y2) ** 2)
                    if c1 != c2:
                        d *= 10
                    edges.append((d, i, N + m))

        init_unionfind(N + M)
        edges.sort()
        cost = 0
        for d, i, j in edges:
            if is_connected(i, j):
                continue
            unite(i, j)
            cost += d
        ret = min(ret, cost)
    return ret
```


[[PAST1L]]
