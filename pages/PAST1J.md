
[J - 地ならし](https://atcoder.jp/contests/past201912-open/tasks/past201912_j)
- ![image](https://gyazo.com/35e2c2626e0ea16ae8009726cef684e2/thumb/1000)

- 考えたこと
    - 経由地点があるのでY字の交差点から3地点への距離を求めて和の最小なものを選ぶ
    - コストが辺ではなく頂点に乗っているが、まあ[[ダイクストラ法]]的にコストの安い方から探索していけば良いだろう
    - O(V^2logV)なので間に合う
- 公式解説
    - [[シュタイナー木]]
- AC
    - グラフを構築してダイクストラ法で3つの端点からone_to_allの距離を求める
    - これは交差点を3回数えてるので2回分を差し引く
    - 得られたY字路のコストの最小値を答える
python

```
def solve(H, W, AS):
    from collections import defaultdict
    edges = defaultdict(dict)
    for x in range(W):
        for y in range(H):
            pos = y * W + x
            if x < W - 1:
                edges[pos + 1][pos] = AS[y][x]
            if x > 0:
                edges[pos - 1][pos] = AS[y][x]
            if y < H - 1:
                edges[pos + W][pos] = AS[y][x]
            if y > 0:
                edges[pos - W][pos] = AS[y][x]
    d1 = one_to_all(W - 1, H * W, edges)
    d2 = one_to_all(W * (H - 1), H * W, edges)
    d3 = one_to_all(W * H - 1, H * W, edges)
    INF = 9223372036854775807
    ret = INF
    for x in range(W):
        for y in range(H):
            pos = y * W + x
            v = d1[pos] + d2[pos] + d3[pos] - 2 * AS[y][x]
            if v < ret:
                ret = v

    return ret
```


- [[最短経路問題]]
- [[一本道ではない最短経路]]

[[第一回 アルゴリズム実技検定]]
