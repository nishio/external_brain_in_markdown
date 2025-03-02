---
title: "ABC154E_old"
---

python

```
def solve(N, K):
    """
    >>> solve(9, 1)
    9
    >>> solve(5, 1)
    5     
    """
    x = N
    digits = []
    while x:
        x, r = divmod(x, 10)
        digits.append(r)
    digits.reverse()
    numDigits = len(digits)

    isBorder = True
    isHead = True
    index = 0
    ret = 0
    for i in range(10):
        if i == 0:
            continue
        if i > digits[index]:
            break
        ret += 1

    return ret
```


python

```
def solve(N, K):
    """
    >>> solve(9, 1)
    9
    >>> solve(5, 1)
    5
    """
    x = N
    digits = []
    while x:
        x, r = divmod(x, 10)
        digits.append(r)
    digits.reverse()
    numDigits = len(digits)

    def f(isBorder, isHead, index):
        ret = 0
        for i in range(10):
            if i == 0:
                continue
            if i > digits[index]:
                break
            ret += 1
        return ret

    return f(True, True, 0)
```


python

```
Failed example:
    solve(10, 1)
Expected:
    10
Got:
    1
```


python

```
        for i in range(10):
            if i == 0:
                if isHead and index == numDigits - 1:
                    continue
                else:
                    ret += f(False, True, 1)
```


python

```
Failed example:
    solve(10, 1)
Expected:
    10
Got:
    2
```


python

```
            if isBorder and i > digits[index]:
                break
```


python

```
Failed example:
    solve(10, 1)
Expected:
    10
Got:
    11
```


python

```
        for i in range(10):
            if i == 0:
                if isHead and index == numDigits - 1:
                    continue
                else:
                    ret += f(False, True, 1)
            if isBorder and i > digits[index]:
                break
            ret += 1
        debug("ret: ret, isBorder, isHead, index: ",
              ret, isBorder, isHead, index)
        return ret
```


python

```
    >>> solve(100, 1)
    19
```


python

```
        for i in range(10):
            if i == 0:
                if isHead and index == numDigits - 1:
                    continue
                else:
                    ret += f(False, True, index + 1)
                    continue
            if isBorder and i > digits[index]:
                break
            ret += 1
```


python

```
                if isHead and index == numDigits - 1:
                    continue
                else:
                    xs = f(False, True, index + 1)
                    for j in range(K + 1):
                        ret[j] += xs[j]
                    continue
```


python

```
    >>> solve(25, 2)
    14
```


python

```
Failed example:
    solve(25, 2)
Expected:
    14
Got:
    0
```


