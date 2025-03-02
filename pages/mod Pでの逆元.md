---
title: "mod Pでの逆元"
---

フェルマーの小定理
- $a^{p-1}\equiv 1{\pmod {p}}$
を変形して
- $a \times a^{p-2}\equiv 1{\pmod {p}}$
なので
- $a^{-1} \equiv a^{p-2} {\pmod {p}}$

Python: `pow(a, p - 2, p)`
Python3.8から素直に `pow(a, -1, p)`できる

フェルマーの小定理はPが素数であることを要求する
- 素数でない場合には[[拡張ユークリッド互除法]]を使う　[[Pが素数でないmod P]]
- この場合はaとpが互いに素であれば良い
python

```
def mod_inverse_ee(a, m):
    """
     Solve ax mod m = 1 with extended euclidean.
     x = a^-1.
     """
    x, y, g = extended_euclidean(a, m)
    assert g == 1
    return x % m
```

- [[剰余群での除算]]


> nのmodulo pでの逆元は[[フェルマーの小定理]]より
>  pow(n, p-2, p)
>  で求められます。計算量はO(logp)です。[[二項係数]]とかでよく使います。
[https://qiita.com/Kentaro_okumura/items/5b95b767a2e691cd5482](https://qiita.com/Kentaro_okumura/items/5b95b767a2e691cd5482)
