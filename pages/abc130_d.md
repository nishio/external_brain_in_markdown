
[D - Enough Array](https://atcoder.jp/contests/abc130/tasks/abc130_d)
- 数列が与えられて、その数列の連続部分列で、総和がK以上のものを数え上げる
- 数列は最大10^5まで
- まずは素朴なもの(といっても[[累積和]]は使ってしまったのでもっと素朴な書き方ができるが…)
python

```
def solve(N, K, XS):
    from itertools import accumulate
    acc = [0] + list(accumulate(XS))
    ret = 0
    for i in range(N):
        for j in range(i + 1, N + 1):
            if acc[j] - acc[i] >= K:
                ret += 1
    return ret
```


で、これだと二乗のオーダーで10^10なので、片方をlog Nに変える
- [[bisect]]
python

```
def solve(N, K, XS):
    import bisect
    from itertools import accumulate
    acc = [0] + list(accumulate(XS))
    ret = 0
    for i in range(N):
        lb = acc[i] + K
        j = bisect.bisect_left(acc, lb)
        ret += N + 1 - j
    return ret
```

AC [提出 #15126807 - AtCoder Beginner Contest 130](https://atcoder.jp/contests/abc130/submissions/15126807)
