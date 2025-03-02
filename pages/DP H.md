---
title: "DP H"
---

[H - Grid 1](https://atcoder.jp/contests/dp/tasks/dp_h)
- グリッドに障害物が置かれている、右または下に移動することで左上から右下に至る経路はいくつあるか、という問題
- [[経路数え上げ]]
- グリッド上の点を定義域とし、その点へ至る経路の個数を値とするDP
from [[動的計画法]]
DP_H
H:

python

```
def solve(H, W, data):
    score = [[0] * (W + 1) for i in range(H + 1)]
    score[0][1] = 1
    for y in range(1, H + 1):
        for x in range(1, W + 1):
            if data[y - 1][x - 1] == ord("#"):
                score[y][x] = 0
            else:
                score[y][x] = (score[y - 1][x] + score[y][x - 1]) % MOD
    return score[H][W]
```

