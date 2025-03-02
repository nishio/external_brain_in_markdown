
from [[第四回 アルゴリズム実技検定]]
PAST4F
[F - 構文解析](https://atcoder.jp/contests/past202010-open/tasks/past202010_f)
- 上または下と比べて出現回数が同じならAMBIGUOUS
python

```
def solve(N, K, SS):
    from collections import Counter
    c = Counter(SS).most_common()
    K -= 1
    ck, ckv = c[K]
    if K > 0:
        _, pv = c[K - 1]
        if pv == ckv:
            return "AMBIGUOUS"
    if K < len(c) - 1:
        _, pv = c[K + 1]
        if pv == ckv:
            return "AMBIGUOUS"
    return ck
```

