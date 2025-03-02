---
title: "np.arrayが遅い"
---

まとめ
- np.array はリストに比べて2倍ほど要素アクセスが遅い
    - [[numpyの添え字アクセスは遅い]]
- 累積和を計算するコードを作りnumbaでコンパイルするとnp.arrayを使った側が速くなった
    - 速くなりすぎ感があるので今度もう少しちゃんと調べたい
- numbaを調べてた時に書いたのでnumbaの話ばかりだが、Numpyを使う上ではまず[[ループをNumpyに任せる]]ことを優先した方が良い

[[numba]]に渡すために[[RBST]]の今までリストで作ってたところをnp.arrayに置き換えたらやたら遅くなった
python

```
# 6.080607408sec
self.vals = np.repeat(SUM_UNITY, MAX_NODE_ID)
self.sizes = np.ones(MAX_NODE_ID, dtype=np.int)
self.sums = np.repeat(SUM_UNITY, MAX_NODE_ID)
self.lefts = np.zeros(MAX_NODE_ID, dtype=np.int)
self.rights = np.zeros(MAX_NODE_ID, dtype=np.int)
# 2.765020115
# self.vals = [SUM_UNITY] * MAX_NODE_ID
# self.sizes = [1] * MAX_NODE_ID
# self.sums = [SUM_UNITY] * MAX_NODE_ID
# self.lefts = [0] * MAX_NODE_ID
# self.rights = [0] * MAX_NODE_ID
```


調べてみると添え字アクセスが2倍ちょい遅い: list 57.4 ms / np.array 134 ms
:

```
In [34]: %%timeit
    ...: N = 1000_000; xs = [0] * N
    ...: for i in range(N):
    ...:     xs[i] = xs[i]
    ...: 
    ...: 
    ...: 
57.4 ms ± 454 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)

In [35]: %%timeit
    ...: N = 1000_000; xs = np.zeros(N)
    ...: for i in range(N):
    ...:     xs[i] = xs[i]
    ...: 
    ...: 
    ...: 
134 ms ± 1.55 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
```


これは本題でないグローバルアクセスが遅い現象: global 155 ms / local 135 ms
:

```
In [37]: def foo():
    ...:     for i in range(N):
    ...:         xs[i] = xs[i]
    
In [40]: %timeit foo()
155 ms ± 2.05 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)

In [44]: def foo(xs):
    ...:     for i in range(N):
    ...:         xs[i] = xs[i]
    ...: 
    ...:         

In [45]: %timeit foo(xs)
135 ms ± 2.84 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
```


numbaコンパイルすれば速くなるが、これは速くなりすぎ(np.array: 255 ns)なので最適化でループごと消えてそう
list: 1.69 s、かえって遅くなる。
この使い方はNumbaPendingDeprecationWarning:
Encountered the use of a type that is scheduled for deprecation: type 'reflected list' found for argument 'xs' of function 'foo'. For more information visit [http://numba.pydata.org/numba-doc/latest/reference/deprecation.html#deprecation-of-reflection-for-list-and-set-types](http://numba.pydata.org/numba-doc/latest/reference/deprecation.html#deprecation-of-reflection-for-list-and-set-types)
:

```
In [46]: foo = numba.njit(foo)

In [47]: %timeit foo(xs)
255 ns ± 2.11 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)

n [58]: numba.void(numba.typeof([0]))
Out[58]: (reflected list(int64),) -> none

In [59]: def foo(xs):
    ...:     for i in range(N):
    ...:         xs[i] = xs[i]
    ...: 
    ...:         

In [60]: foo = numba.njit(numba.void(numba.typeof([0])))(foo)
...NumbaPendingDeprecationWarning: 
Encountered the use of a type that is scheduled for deprecation: type 'reflected list' found for argument 'xs' of function 'foo'.

For more information visit http://numba.pydata.org/numba-doc/latest/reference/deprecation.html#deprecation-of-reflection-for-list-and-set-types
...
In [63]: %timeit foo(xs)
1.69 s ± 12 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
```


最適化で消えないようにしてコンパイルした
np.arrayの方が3000倍ほど速くなった: list: 1.69 s / np.array 549 µs
- 本当か？
:

```
In [85]: xs = np.zeros(N, np.int32)
    ...: @numba.njit(numba.i4(numba.i4[:]))
    ...: def foo(xs):
    ...:     for i in range(1, N):
    ...:         xs[i] += xs[i - 1]
    ...:     return xs[N - 1]
    ...: 
    ...: 

In [86]: %timeit foo(xs)
549 µs ± 10.6 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)

In [87]: xs = [0] * N
    ...: @numba.njit(numba.i4(numba.typeof([0])))
    ...: def foo(xs):
    ...:     for i in range(1, N):
    ...:         xs[i] += xs[i - 1]
    ...:     return xs[N - 1]

In [88]: %timeit foo(xs)
1.69 s ± 11.4 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
```


:

```
In [89]: xs = [0] * N
    ...: def foo(xs):
    ...:     for i in range(1, N):
    ...:         xs[i] += xs[i - 1]
    ...:     return xs[N - 1]
    ...: 
    ...: 

In [90]: %timeit foo(xs)
116 ms ± 2.27 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)

In [91]: xs = np.zeros(N, np.int32)
    ...: def foo(xs):
    ...:     for i in range(1, N):
    ...:         xs[i] += xs[i - 1]
    ...:     return xs[N - 1]
    ...: 
    ...: 

In [92]: %timeit foo(xs)
280 ms ± 5.67 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
```

