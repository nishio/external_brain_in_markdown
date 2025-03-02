---
title: "PAST3J"
---

from [[第三回 アルゴリズム実技検定]]
PAST3J
- 流れてくる数値が今まで取ったどれよりも大きい時だけ取るエージェントが複数並んでる時に、どの数値を誰が取るか答える問題。
- エージェントごとに「これ以上なら取る」という数値を持っていて、「流れてきた数値xよりも小さい値の最も左のエージェント」を返せば良い。
    - つまりこれはソート済み配列からの効率良い探索。
    - 二分探索の方法をPythonで調べたら標準ライブラリに[[bisect]]ってのがあったので初めて使った。
python

```
from bisect import bisect_right
N, M = [int(x) for x in input().split()]
XS = [int(x) for x in input().split()]

scores = [0] * N

for x in XS:
    # need to nagate to keep asc. order
    # print("come", x)
    i = bisect_right(scores, -x)
    if i == N:
        print(-1)
    else:
        print(i + 1)
        scores[i] = -x
        # print(scores)
```

