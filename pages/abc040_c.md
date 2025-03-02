---
title: "abc040_c"
---

[[DP A]]で見た問題。同じ解き方をしても面白くないので「動的計画法なのに配列を確保しない」を試して列の長さが短い時にREした
[C - 柱柱柱柱柱](https://atcoder.jp/contests/abc040/tasks/abc040_c)
python

```
def solve(N, XS):
    if N == 1:
        return 0
    a = abs(XS[1] - XS[0])
    if N == 2:
        return a
    b = abs(XS[2] - XS[0])
    if N == 3:
        return b
    for i in range(3, N):
        v = min(
            a + abs(XS[i - 2] - XS[i]),
            b + abs(XS[i - 1] - XS[i]),
        )
        a = b
        b = v
    return v
```


[https://atcoder.jp/contests/abc040/submissions/15212600](https://atcoder.jp/contests/abc040/submissions/15212600)
