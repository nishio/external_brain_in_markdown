
2020-08-05
- Python3: 960 ms
- PyPy3: 92 ms
python

```
def f1(x):
    return x


def f2(x):
    ret = 0
    for i in range(10000):
        ret ^= f1(x)
    return ret

def f3(x):
    ret = 0
    for i in range(1000):
        ret ^= f2(x)
    return ret

print(f3(int(input())))
```


- 1000: PyPy3: 92 ms
- 10000: PyPy3: 164 ms
- 100000: PyPy3: 923 ms

- 1000: Cython: 387 ms
    - あれ？意外と速度が出ないな？何が勘違いしてるかな？
python

```
cdef f1(int x):
    return x


cdef f2(int x):
    cdef int ret = 0
    cdef int i
    for i in range(10000):
        ret ^= f1(x)
    return ret

  
cdef f3(int x):
    cdef int ret = 0
    cdef int i
    for i in range(1000):
        ret ^= f2(x)
    return ret

print(f3(int(input())))
```

