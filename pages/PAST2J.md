---
title: "PAST2J"
---

from [[第二回 アルゴリズム実技検定]]
![image](https://gyazo.com/b4d2ae6d4c49a41f64ced937f0f5dbae/thumb/1000)
[J - 文字列解析](https://atcoder.jp/contests/past202004-open/tasks/past202004_j)

PAST2J
- 括弧で囲われた範囲を処理する関数を使って再帰呼び出しすれば良い
- 文字列を直接編集するのではなく添え字でアクセスする
- AC
python

```
def solve(S):
    N = len(S)
    cur = 0
    ret = []

    def parse_palen():
        nonlocal cur
        cur += 1
        ret = []
        while cur < N:
            c = S[cur]
            if c == ")":
                s = "".join(ret)
                s2 = "".join(reversed(s))
                return s + s2
            elif c == "(":
                ret.append(parse_palen())
            else:
                ret.append(c)
            cur += 1

    while cur < N:
        c = S[cur]
        if c == "(":
            ret.append(parse_palen())
        else:
            ret.append(c)
        cur += 1
    return "".join(ret)
```


9min
