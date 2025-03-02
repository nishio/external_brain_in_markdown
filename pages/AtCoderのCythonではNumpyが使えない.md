---
title: "AtCoderのCythonではNumpyが使えない"
---

cython

```
cimport numpy as np
```

:

```
./Main.c:600:10: fatal error: numpy/arrayobject.h: No such file or directory
  600 | #include "numpy/arrayobject.h"
      |          ^~~~~~~~~~~~~~~~~~~~~
compilation terminated.
```


[コードテスト - AtCoder Beginner Contest 172](https://atcoder.jp/contests/abc172/custom_test)で試した
