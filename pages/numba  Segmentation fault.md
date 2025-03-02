
python

```
import sys


def foo(x):
    x[0] = 1
    return 1


if sys.argv[-1] == "-c":
    # numba compile
    print("compiling")
    from numba.pycc import CC
    cc = CC('my_module')
    cc.export('foo', 'i8(i8[:])')(foo)
    # b1: bool, i4: int32, i8: int64, double: f8, [:], [:, :]
    cc.compile()
    exit()
else:
    from my_module import foo
    x = [0]
    foo(x)
```


OK
python

```
    import numpy as np
    x = np.zeros(1, dtype=np.int64)
    print(foo(x)) 
```


[[numba]]
