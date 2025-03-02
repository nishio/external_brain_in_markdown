---
title: "DP O"
---

[O - Matching](https://atcoder.jp/contests/dp/tasks/dp_o)
- 21個のものの順列のうち、特定の条件を満たすものを数え上げる問題
- 先頭を一つ決めて、残りの20個の順列を考える場合に「使えるもの」が21通りある
    - というわけで「使えるもの」を定義域とし、条件を満たすものの個数を値とするDP
    - 「使えるもの」は高々21個の集合の部分集合なので2^21、およそ10^7
    - 小さい集合の部分集合を列挙するのはビット演算を使うと速い(生Pythonではそれほどでもないが)
    - [[bitDP]]と呼ぶ人もいるのかな
- 生PythonではTLEしそうだったが、PyPyなら AC
python

```
def solve(N, data):
    FULLBIT = (1 << N) - 1
    memo = [-1] * (1 << N)

    def f(cursor, available):
        if cursor == N:
            return 1
        ret = memo[available]
        if ret != -1:
            return ret
        ret = 0
        j = 0
        m = available
        while m:
            if m & 1:
                # available woman
                if data[cursor * N + j]:
                    # acceptable
                    ret += f(cursor + 1, available ^ (1 << j))
            j += 1
            m //= 2
        ret %= MOD
        memo[available] = ret
        return ret

    return f(0, FULLBIT)
```

[https://atcoder.jp/contests/dp/submissions/15068618](https://atcoder.jp/contests/dp/submissions/15068618)
