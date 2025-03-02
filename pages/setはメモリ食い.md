---
title: "setはメモリ食い"
---

Pythonのsetは1エントリーあたり90バイトも食っている。
10Mエントリー前後で[[atcoder]]の1024MBのメモリ制限に引っかかる。
定義域が`[0, N)`なら`np.zeros(N, np.bool_)`がよい。[[座標圧縮]]でその形に持ち込むのも良さそう。

[[mprof]]
python

```
x = set()
for i in range(9_000_000):
    x.add(i)
```

- ![image](https://gyazo.com/afd0afef705664b82f9b3628c428add9/thumb/1000)

python

```
import numpy as np
x = np.zeros(9_000_000, np.bool_)
for i in range(9_000_000):
    x[i] = 1
```

- ![image](https://gyazo.com/e229d1c6443dd898728e827e4419e730/thumb/1000)
