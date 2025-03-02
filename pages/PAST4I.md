---
title: "PAST4I"
---

from [[第四回 アルゴリズム実技検定]]
PAST4I
[I - ピザ](https://atcoder.jp/contests/past202010-open/tasks/past202010_i)
- 考えたこと
    - やっと巨大なNの問題
        - [[円周のRange Sum]]が最大になるところを探す
        - 2倍にして累積和
        - それでも始点と終点が自由だと二乗のオーダー
        - [[しゃくとり法]]をする
        - イコールの時にどっちをすればいい？
            - 縮める？
            - イコールの時は答えが0だから終わっていいのか
            - 通ったのでいいや
python

```
def solve(N, AS):
    import sys
    INF = sys.maxsize

    from itertools import accumulate
    acc = list(accumulate(AS + AS)) + [0]

    def rangeSum(start, end):
        return acc[end - 1] - acc[start - 1]

    start = 0
    end = 1
    ret = INF
    total = rangeSum(0, N)
    while True:
        x = rangeSum(start, end)
        y = total - x
        d = x - y
        ret = min(abs(d), ret)
        if d < 0:
            if end == 2 * N - 1:
                break
            end += 1
        else:
            start += 1
    return ret
```

