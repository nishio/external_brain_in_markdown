---
title: "PyPyの関数呼び出しは遅い"
---

python

```
import sys

sys.setrecursionlimit(10**6)

def foo(x):
  if x == 0: return 0
  return foo(x - 1)

print(foo(10 ** 6 - 10))
```

[コードテスト - Educational DP Contest / DP まとめコンテスト](https://atcoder.jp/contests/dp/custom_test)で試す
- Python: 実行時間 653 ms
- PyPy: 実行時間 1154 ms

#atcoder
