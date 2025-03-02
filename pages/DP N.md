
[N - Slimes](https://atcoder.jp/contests/dp/tasks/dp_n)
- 隣接するものをくっつける
- くっつける順番によってコストが異なる
- コストを最小化する問題
- 領域を定義域とするDP
    - [[DP L]]と同様
    - 領域が指定された時のその領域をくっつける最安コストを値としてDP
- [[累積和]]
python

```
def solve(N, XS):
    accum = list(accumulate(XS)) + [0]
    @lru_cache(maxsize=None)
    def sub(L, R):
        if L == R:
            return 0
        ret = INF
        for x in range(L, R):
            v = sub(L, x) + sub(x + 1, R)
            if v < ret:
                ret = v
        return ret + accum[R] - accum[L - 1]
    return sub(0, N - 1)
```


Cython
python

```
cdef long long[400 * 400] table
cdef long long[410] accum

cdef sub(long L, long R):
    cdef long long ret
    if L == R:
        return 0
    ret = table[L * 400 + R]
    if ret != 0:
        return ret

    ret = INF
    for x in range(L, R):
        v = sub(L, x) + sub(x + 1, R)
        if v < ret:
            ret = v
    ret += accum[R + 1] - accum[L]
    table[L * 400 + R] = ret
    return ret

cdef solve(N, XS):
    cdef long i
    cdef long long v
    v = 0
    accum[0] = 0
    for i in range(N):
        v += XS[i]
        accum[i + 1] = v
    return sub(0, N - 1)
```

[https://atcoder.jp/contests/dp/submissions/15066323](https://atcoder.jp/contests/dp/submissions/15066323)
