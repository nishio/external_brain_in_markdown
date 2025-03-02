---
title: "DP I"
---

[I - Coins](https://atcoder.jp/contests/dp/tasks/dp_i)
- コインが何枚かあり、それぞれの表になる確率が与えられる、表の枚数が裏より多くなる確率を求める問題
- 先頭からコインを見て行った時に、表である枚数を定義域とし、その確率を値とするDP
from [[動的計画法]]

- [[確率DP]]
- Python TLE PyPy AC
python

```
def solve(N, probs):
    m = [0.0] * (N + 1)
    m[0] = 1.0

    for i in range(N):
        n = [0.0] * (N + 1)
        for j in range(N):
            n[j + 1] += m[j] * probs[i]
        for j in range(N + 1):
            n[j] += m[j] * (1 - probs[i])
        m = n
    return sum(m[N // 2 + 1:])
```

[https://atcoder.jp/contests/dp/submissions/14880753](https://atcoder.jp/contests/dp/submissions/14880753)
