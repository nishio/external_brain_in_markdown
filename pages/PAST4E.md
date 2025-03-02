---
title: "PAST4E"
---

from [[第四回 アルゴリズム実技検定]]
PAST4E
[E - アナグラム](https://atcoder.jp/contests/past202010-open/tasks/past202010_e)
- 考えたこと
    - 5だから全探索
python

```
def solve(N, S):
    from itertools import permutations
    rS = "".join(reversed(S))
    for p in permutations(S):
        ret = "".join(p)
        if ret != S and ret != rS:
            return ret
    return "None"
```

