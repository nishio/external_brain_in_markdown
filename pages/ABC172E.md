---
title: "ABC172E"
---

[E - NEQ](https://atcoder.jp/contests/abc172/tasks/abc172_e)
- ![image](https://gyazo.com/a43c39f8615db563d14106992866b62e/thumb/1000)


-----
数え上げ問題をみて、[[動的計画法]]かな？と思ったが[[余事象を引く]]方が楽なパターン

最近、一周回って「まずは素朴に書いていいんじゃない？」って思うようになってきた。問題文を読み間違えてる時に素早く気づけるし、TLEしたので複雑なアルゴリズムを書く場合にもテストコード生成させられる
python

```
def blute(N, M):
    """
    >>> blute(2, 2)
    2

    >>> blute(2, 3)
    18
    """
    from itertools import permutations
    nums = range(M)
    count = 0
    for a in permutations(nums, N):
        for b in permutations(nums, N):
            if all(a[i] != b[i] for i in range(N)):
                count += 1
    print(count)
```


python

```
for M in range(1, 10):
    for N in range(1, M + 1):
        print("N, M, f = ", N, M, blute(N, M))
```


:

```
N, M, f =  1 1 0
N, M, f =  1 2 2
N, M, f =  2 2 2
N, M, f =  1 3 6
N, M, f =  2 3 18
N, M, f =  3 3 12
N, M, f =  1 4 12
N, M, f =  2 4 84
N, M, f =  3 4 264
N, M, f =  4 4 216
N, M, f =  1 5 20
N, M, f =  2 5 260
N, M, f =  3 5 1920
N, M, f =  4 5 6360
N, M, f =  5 5 5280
N, M, f =  1 6 30
N, M, f =  2 6 630
N, M, f =  3 6 8520
N, M, f =  4 6 65160
N, M, f =  5 6 222480
N, M, f =  6 6 190800
N, M, f =  1 7 42
N, M, f =  2 7 1302
N, M, f =  3 7 28140
N, M, f =  4 7 390600
N, M, f =  5 7 3059280
```


f(N, M)
f(1, M) = M * (M - 1)

python

```
for M in range(2, 100):
    r1 = blute(1, M)
    r2 = blute(2, M)
    r3 = blute(3, M)
    debug("r2/r1, r3/r2, r3/r1", r2/r1, r3/r2, r3/r1)
```


:

```
r2/r1, r3/r2, r3/r1 1.0 0.0 0.0
r2/r1, r3/r2, r3/r1 3.0 0.6666666666666666 2.0
r2/r1, r3/r2, r3/r1 7.0 3.142857142857143 22.0
r2/r1, r3/r2, r3/r1 13.0 7.384615384615385 96.0
r2/r1, r3/r2, r3/r1 21.0 13.523809523809524 284.0
r2/r1, r3/r2, r3/r1 31.0 21.612903225806452 670.0
r2/r1, r3/r2, r3/r1 43.0 31.674418604651162 1362.0
r2/r1, r3/r2, r3/r1 57.0 43.719298245614034 2492.0
r2/r1, r3/r2, r3/r1 73.0 57.75342465753425 4216.0
r2/r1, r3/r2, r3/r1 91.0 73.78021978021978 6714.0
r2/r1, r3/r2, r3/r1 111.0 91.8018018018018 10190.0
```


:

```
In [11]: xs = np.array([0.0, 2.0, 22.0, 96.0, 284.0, 670.0, 1362.0, 2492.0])
In [12]: xs[1:] - xs[:-1]
Out[12]: array([   2.,   20.,   74.,  188.,  386.,  692., 1130.])
In [14]: dxs = xs[1:] - xs[:-1]

In [15]: dxs[1:] - dxs[:-1]
Out[15]: array([ 18.,  54., 114., 198., 306., 438.])
In [16]: ddxs = dxs[1:] - dxs[:-1]

In [17]: ddxs[1:] - ddxs[:-1]
Out[17]: array([ 36.,  60.,  84., 108., 132.])
In [19]: dddxs = ddxs[1:] - ddxs[:-1]

In [20]: dddxs[1:] - dddxs[:-1]
Out[20]: array([24., 24., 24., 24.])
```



