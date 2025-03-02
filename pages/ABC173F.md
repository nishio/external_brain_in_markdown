---
title: "ABC173F"
---

- 木はちょうど頂点数-1本の辺を持つ
- よって森に含まれる木の個数は頂点数vと辺の数eから求められる
    - $f(L,R) = v(L,R) - e(L,R)$
    - [[閉路のないグラフ]]の[[連結成分の個数]]
- [[演算順序の変更]]
    - $\sum_L \sum_R f(L,R) = \sum_L \sum_R v(L,R) - \sum_L \sum_R e(L,R)$
    - $\sum_L \sum_R 1_{L \le i \le R}  = (N - (i-1)) ((i-1) + 1)$

python

```
def main():
    v = 0
    e = 0
    N = int(input())
    for i in range(N):
        v += (N - i) * (i + 1)

    for i in range(N - 1):
        v1, v2 = sorted(map(int, input().split()))
        v1 -= 1
        v2 -= 1
        e += (N - v2) * (v1 + 1)

    debug(": e, v", e, v)
    print(v - e)
```


[https://atcoder.jp/contests/abc173/submissions/15029754](https://atcoder.jp/contests/abc173/submissions/15029754)
