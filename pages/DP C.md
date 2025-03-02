---
title: "DP C"
---

[C - Vacation](https://atcoder.jp/contests/dp/tasks/dp_c)
- 3つの数列から最も和が大きくなるように取りたい
- ただし同じ数列から連続して取ることはできない
- 直前が3通りのどれであったか、を定義域とし、その場合の和を値とするDP
from [[動的計画法]]
DP_C
- PyPy 144 ms
python

```
def solve(N, scores):
    last_score = scores[0]
    for i in range(1, N):
        next_score = [
            max(last_score[1], last_score[2]) + scores[i][0],
            max(last_score[2], last_score[0]) + scores[i][1],
            max(last_score[0], last_score[1]) + scores[i][2],
        ]
        last_score = next_score
    return max(last_score)
```

