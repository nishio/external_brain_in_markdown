---
title: "Python list v.s. set"
---

リストへのappendに比べて、setへのaddは70nsほど遅い
- ハッシュ値の計算コストなど
- これはC世界のコストなのでPyPyとかでも縮みにくい
    - 結果[[ABC176]]で発生したように「setでuniqueにするよりループを空回りさせた方が速い」という現象が起こる
python

```
In [77]: %%timeit
    ...: xs = []
    ...: xs.append(1)
    ...: 
71.9 ns ± 1.01 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)

In [78]: %%timeit
    ...: xs = set()
    ...: xs.add(1)
    ...: 
141 ns ± 0.457 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)
```

