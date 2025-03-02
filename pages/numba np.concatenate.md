---
title: "numba np.concatenate"
---

In [[numba]] world, [[np.concatenate]] can not concatenate np.array and list. (as of numba 0.50)

`np.concatenate(): expecting a non-empty tuple of arrays, got Tuple(array(int64, 1d, C), list(int64))`

python

```
import numba
import numpy as np


@numba.njit
def foo():
    x = np.array([1, 2, 3])

    # OK
    print(np.concatenate((x, x)))

    # NG
    print(np.concatenate((x, [1, 2, 3])))
    # TypeError: np.concatenate(): expecting a non-empty tuple of arrays, got Tuple(array(int64, 1d, C), list(int64))


foo()
```


