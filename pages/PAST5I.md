
[I - 避難計画](https://atcoder.jp/contests/past202012-open/tasks/past202012_i)
![image](https://gyazo.com/01513f650068f7946cc04b839444666a/thumb/1000)
- 初回考察
    - 標高の高い方から低い方へしか動けない
        - 有向グラフ
    - ゴールがたくさん
        - コスト0の辺で束ねる？
            - [[ゴールを一つにする]]
        - 各ゴールからone to allの[[ダイクストラ法]]？
        - 後者をやって、ダメなら前者にしよう
    - 考察完了
- 実装
    - どうせダイクストラ法やるなら前者の実装をする追加工数は大したことないので後者をやるメリットはないなと判断
    - 前者の実装をする追加コード : `(1)`
- AC
python

```
def solve(N, M, K, HS, CS, ABS):
    from collections import defaultdict
    edges = defaultdict(dict)
    for i in range(M):
        frm, to = ABS[i]
        frm -= 1
        to -= 1
        if HS[frm] < HS[to]:
            to, frm = frm, to
        # reversed edge
        edges[to][frm] = 1

    goal = N
    for c in CS:
        edges[goal][c - 1] = 0  # (1)

    distances = one_to_all(goal, N + 1, edges)
    INF = 9223372036854775807
    for i in range(N):
        d = distances[i]
        if d == INF:
            d = -1
        print(d)
```

