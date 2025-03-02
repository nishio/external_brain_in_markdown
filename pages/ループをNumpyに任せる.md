
Numpyを使う上ではループをNumpy側でやるかPython側でやるかが速度に大きく影響する

sum(xs) v.s. xs.sum(): xs.sum()が178倍早い
- sum(xs)ではPython側でnp.arrayを単なる汎用のiterableだとみなして合計している
- xs.sum()では、Numpy側が、np.arrayであることを理解して合計している
- 後者の場合、値をPyFloatオブジェクトにするコストが丸ごと不要になる
python

```
In [3]: xs = np.arange(1000_000)

In [4]: %timeit sum(xs)
80.5 ms ± 210 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)

In [5]: %timeit xs.sum()
448 µs ± 4.18 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```


添え字アクセスでのインクリメントと、ブロードキャストでのインクリメント、後者が205倍速い
- (後者はベンチマークの都合でローカル変数になってるので少しフェアじゃない)
- [Broadcasting — NumPy v1.19 Manual](https://numpy.org/doc/stable/user/basics.broadcasting.html)
python

```
In [7]: %%timeit
   ...: for i in range(1000_000):
   ...:     xs[i] += 1
   ...: 
284 ms ± 1.88 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)

In [11]: %%timeit
    ...: xs = np.arange(1000_000)
    ...: xs += 1
    ...: 
1.38 ms ± 25.3 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)
```

