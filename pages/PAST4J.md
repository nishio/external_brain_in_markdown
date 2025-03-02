
from [[第四回 アルゴリズム実技検定]]
PAST4J
[J - ワープ](https://atcoder.jp/contests/past202010-open/tasks/past202010_j)
- 考えたこと
    - 連結単純無向グラフ
    - ワープ
    - 辺は10^5だが、ワープを明示的に辺にすると10^10
    - ワープを使う回数に制限があるのだろう
    - いや、優先度キューで[[ダイクストラ法]]すれば間に合うか
    - 間に合いませんな
    - もう少し考察
        - スタートと違う色の街には初手でワープ
            - その後の探索で同じワープが必要になることはない、スコアは必ず悪い
            - 戻りジャンプも同様か
        - ダメだ、答えが合わない、保留
    - 修正前は31TLE
    - 修正後は6WA, 1TLE
        - よくなってる？
        - ジャンプを各色1回しか使わないのの何が悪いのか
            - 片道じゃなくて両方向だ
    - それでも1TLEしそう
        - そのとおり
        - どういう時にそうなる？
    - 毎回heappushしないでまとめてheapify
        - ダメか
        - 33TLEに増えた
    - visitedの追加
        - 通った！
python

```
def solve(N, M, X, S, ABC):
    INF = 1e+99
    from collections import defaultdict
    edges = defaultdict(dict)
    for A, B, C in ABC:
        edges[A - 1][B - 1] = C
        edges[B - 1][A - 1] = C

    warps = [[], [], []]
    for i in range(N):
        warps[S[i]].append(i)

    usedWarp = set()
    GOAL = N - 1
    START = 0

    from heapq import heappush, heappop, heapify
    queue = [(0, START)]
    mincost = [INF] * N
    mincost[START] = 0
    visited = [0] * N

    while True:
        cost, pos = heappop(queue)
        if pos == GOAL:
            return cost
        if visited[pos]:
            continue
        visited[pos] = 1
        ep = edges[pos]
        for next in ep:
            nc = cost + ep[next]
            if nc < mincost[next]:
                mincost[next] = nc
                heappush(queue, (nc, next))

        for typ in range(3):
            if typ == S[pos]:
                continue
            warp = S[pos] + typ - 1

            if (S[pos], typ) in usedWarp:
                continue

            c = X[warp]
            usedWarp.add((S[pos], typ))

            nc = cost + c
            for next in warps[typ]:
                if nc < mincost[next]:
                    mincost[next] = nc
                    heappush(queue, (nc, next))
```



[https://twitter.com/maspy_stars/status/1325748032579645441?s=21](https://twitter.com/maspy_stars/status/1325748032579645441?s=21)
- [[arc061_c]]
