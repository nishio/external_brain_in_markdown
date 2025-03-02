---
title: "numpyの添え字アクセスは遅い"
---

添え字指定でのランダムアクセスを繰り返すようなアルゴリズムに関してはnumpy.arrayにするよりリストのままの方が速い
python

```
In [71]: %%timeit
    ...: xs = np.zeros(100)
    ...: xs[0]
    ...: 
696 ns ± 4.94 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)

In [72]: %%timeit
    ...: xs = [0] * 100
    ...: xs[0]
    ...: 
416 ns ± 3.79 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
```
