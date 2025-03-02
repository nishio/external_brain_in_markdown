---
title: "Pandasの辞書的使い方"
---

PandasでNameとValueというカラムのあるCSVを読み込んで、「Nameが特定の値の時のValueを知りたい」という場合。なおNameは一意だとする。
python

```
import pandas as pd
data = pd.read_csv("t.csv")
v = data[data.Name=="1299c1b7a9e0c2bf41af69c449464a49"]
```


以下のように一応期待通りには動く
output

```
                                  Name  Value
9979  1299c1b7a9e0c2bf41af69c449464a49   9979 
```


だけどこれは結構重たい。100万行のCSVから1個選ぶのには64msecくらいかかる。
output

```
%timeit data[data.Name=="1299c1b7a9e0c2bf41af69c449464a49"]
10 loops, best of 3: 64.1 ms per loop
```


こんな時にindex_colを指定すると、以下のようにアクセスできて
python

```
data = pd.read_csv("t.csv", index_col="Name")
v = data.Value["1299c1b7a9e0c2bf41af69c449464a49"]
```


1000倍以上早くなる。
output

```
%timeit data.Value[key]
1 loop, best of 3: 17.9 µs per loop 
```


なお、開くときにindex_colを指定しなかった場合でも、あとから`data.set_index('Name')`することができる。