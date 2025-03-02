
[[numba]]
- [recursion-in-numba Notebook :: Anaconda Cloud](https://anaconda.org/seibert/recursion-in-numba/notebook)
    - > Note that an explicit type signature is required at the moment for Numba's recursion support to work
- [python - Error in recursive function with Numba in nopython mode - Stack Overflow](https://stackoverflow.com/questions/55577893/error-in-recursive-function-with-numba-in-nopython-mode)

NG
python

```
import sys
import numba


def recur(t):
    if t == 0:
        return 1
    return t * recur(t - 1)


if sys.argv[-1] == "-c":
    print("compiling")
    from numba.pycc import CC
    cc = CC('my_module')
    cc.export('recur', 'i8(i8)')(recur)
    cc.compile()
else:
    from my_module import recur
    print(recur(5))
```


:

```
Untyped global name 'recur': cannot determine Numba type of <class 'function'>

File "numbatest.py", line 7:
def recur(t):
    <source elided>
        return 1
    return t * recur(t - 1)
    ^
```


OK
python

```
@numba.njit("i8(i8)")
def recur(t):
```


NG
python

```
def main(x):
    def recur(t):
```

Not Supported
> Numba now supports inner functions as long as they are non-recursive and only called locally, but not passed as argument or returned as result. The use of closure variables (variables defined in outer scopes) within an inner function is also supported.
- [Supported Python features — Numba 0.50.0.dev0+236.g64fbf2b-py3.7-linux-x86_64.egg documentation](https://numba.pydata.org/numba-doc/dev/reference/pysupported.html)
