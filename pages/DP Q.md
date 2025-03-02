---
title: "DP Q"
---

[Q - Flowers](https://atcoder.jp/contests/dp/tasks/dp_q)
- 二つの数列が与えられて、片方の数列の単調増加列になるような部分列すべての中で、もう一つの数列で与えられたスコアの合計が最大になるものを選ぶ問題

- サンプルの小さい問題に関してはこれで解ける
    - このmaxの部分が素朴にO(N)だと全体でN^2になって、10^10だから間に合わない
    - そこでlog Nでmaxを計算できるアルゴリズムを使う
        - [[フェニック木]]
python

```
def solve(N, HS, VS):
    values = [0] * (N + 1)
    for i in range(N):
        h = HS[i]
        values[h] = max(values[:h]) + VS[i]

    return max(values)
```


フェニック木
python

```
def solve(N, HS, VS):
    bit = [0] * (N + 1)  # 1-origin

    def bit_put(pos, val):
        assert pos > 0
        x = pos
        while x <= N:
            bit[x] = max(bit[x], val)
            x += x & -x  # (x & -x) = rightmost 1 = block width

    def bit_max(pos):
        assert pos > 0
        ret = 0
        x = pos
        while x > 0:
            ret = max(ret, bit[x])
            x -= x & -x
        return ret

    for i in range(N):
        h = HS[i]
        m = bit_max(h)
        bit_put(h, m + VS[i])

    return bit_max(N)
```

AC [https://atcoder.jp/contests/dp/submissions/15080447](https://atcoder.jp/contests/dp/submissions/15080447)
