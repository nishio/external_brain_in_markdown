---
title: "PAST3E"
---

from [[第三回 アルゴリズム実技検定]]
PAST3E
E　グラフに色塗りをする問題。バグを入れないように素朴で簡潔に書く
python

```
from collections import defaultdict
N, NUM_EDGES, Q = [int(x) for x in input().split()]
edges = defaultdict(list)
for i in range(NUM_EDGES):
    v1, v2 = [int(x) for x in input().split()]
    edges[v1].append(v2)
    edges[v2].append(v1)
colors = [int(x) for x in input().split()]

for i in range(Q):
    # print(colors)
    f, *v = [int(x) for x in input().split()]
    # print(f, v)
    if f == 1:
        n, = v
        c = colors[n - 1]
        print(c)
        # sprincle
        # print(edges)
        for v in edges[n]:
            colors[v - 1] = c

    elif f == 2:
        n, c = v
        print(colors[n - 1])
        colors[n - 1] = c
```

