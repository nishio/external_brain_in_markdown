---
title: "PAST4H"
---

from [[第四回 アルゴリズム実技検定]]
PAST4H
[H - マス目のカット](https://atcoder.jp/contests/past202010-open/tasks/past202010_h)
- 考えたこと
    - 高々900
        - さらに900掛けても余裕
    - 素朴に全探索しましょう
        - 小さい方から試して、ダメなら大きくしてもダメ
python

```
def solve(N, M, K, data):
    from collections import Counter
    ret = 1
    for y in range(N):
        for x in range(M):
            for w in range(ret + 1, min(N - y + 1, M - x + 1)):
                c = Counter(data[y + i][x + j]
                            for i in range(w)
                            for j in range(w))

                mc = c.most_common(1)[0][1]
                if mc + K >= w * w:
                    ret = w

    return ret
```

