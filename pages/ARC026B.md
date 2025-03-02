---
title: "ARC026B"
---

[B - 完全数](https://atcoder.jp/contests/arc026/tasks/arc026_2)[B - 完全数](https://atcoder.jp/contests/arc026/tasks/arc026_2)
- ![image](https://gyazo.com/3ce26f4ee4e9e40a944a3ec5ac30aee4/thumb/1000)
- 考えたこと
    - あれ？[[約数列挙]]は平方根オーダーでできるから素朴に求めて足しても間に合うのでは？
python

```
def solve(N):
    s = sum(get_divisors(N))
    if s == 2 * N:
        return "Perfect"
    if s < 2 * N:
        return "Deficient"
    return "Abundant"
```

    - AC