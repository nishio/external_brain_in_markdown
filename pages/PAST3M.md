
![image](https://gyazo.com/03933bba41c9b05e4ac79210321a5771/thumb/1000)
[M - 行商計画問題](https://atcoder.jp/contests/past202005-open/tasks/past202005_m)

from [[第三回 アルゴリズム実技検定]]
PAST3M
- 考えたこと
    - 一見、[[巡回セールスマン問題]]だが、頂点数が多いのでもっと効率的なアルゴリズムが使えるのだろうか？
    - 特徴的な問題条件
        - 辺のコストが一定
        - 同じ頂点や辺を何度も使っていい
        - 辺が10^5で抑えられてる
    - [[最小全域木]]が最小コストか？
        - 違う。例えば4つの頂点を回る時、Y字の中心にsがあったらコスト5、パスの端にsがあったら3
    - 木であるか？
        - たぶんそうだと思うが…
- 問題条件見落とし
    - N個の街を巡るのではなくK個の街を巡るのだった
    - 先にK個の各頂点間の距離を求めて巡回セールスマン問題？
- 改めて考える
    - Kは高々16
        - 16!は全探索できない
        - 既に訪問済みの都市2^16と、最後に訪問した都市16の積なら大丈夫
        - →[[bitDP]]
    - 頂点は10^5
        - [[ワーシャルフロイド法]]O(V^3)は無理
        - 辺が10^5で抑えられてる
        - この制約のおかげで[[ダイクストラ法]]O((E+V)log V)が使える
            - [[辺が10^5ならダイクストラ使える]]
    - 16個の頂点からのone to all最短距離をダイクストラで求める
    - 16の頂点間の距離を元に巡回セールスマン問題
        - スタートに戻ってこないパターンなことに注意が必要
- AC
python

```
def solve(N, M, edges, S, K, TS):
    cc = CoordinateCompression(TS)
    v2i, _i2v = cc.compress()

    # dijkstra
    from collections import defaultdict
    distances = defaultdict(dict)
    ds = one_to_all(S, N, edges)
    from_start = {}
    for t in TS:
        from_start[v2i[t]] = ds[t]

    for t in TS:
        ds = one_to_all(t, N, edges)
        for t2 in TS:
            distances[v2i[t]][v2i[t2]] = ds[t2]

    # tsp
    num_vertex = K
    SUBSETS = 2 ** num_vertex
    INF = 9223372036854775807
    memo = [[INF] * num_vertex for _s in range(SUBSETS)]

    for subset in range(1, SUBSETS):
        for v in range(num_vertex):  # new vertex
            mask = 1 << v
            if subset == 1 << v:
                # previous vertex is start
                memo[subset][v] = min(
                    memo[subset][v],
                    from_start[v])
            elif subset & mask:  # new subset includes v
                for u in range(num_vertex):
                    memo[subset][v] = min(
                        memo[subset][v],
                        memo[subset ^ mask][u] + distances[u][v])
    return min(memo[-1])
```


[[辺が10^5の制約]]
