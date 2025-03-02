
名前がよくない自覚はあるが、良い名前を思いついてない
`up(pos): pos // (pos & -pos)`
python

```
>>> debugprint([pos // (pos & -pos) if pos else 0 for pos in table])
|                       1                       |
|           1           |           3           |
|     1     |     5     |     3     |     7     |
|  1  |  9  |  5  |  11 |  3  |  13 |  7  |  15 |
|1 |17|9 |19|5 |21|11|23|3 |25|13|27|7 |29|15|31|
```


python

```
>>> debugprint(table)
|                       1                       |
|           2           |           3           |
|     4     |     5     |     6     |     7     |
|  8  |  9  |  10 |  11 |  12 |  13 |  14 |  15 |
|16|17|18|19|20|21|22|23|24|25|26|27|28|29|30|31|
```


> (N+L)/(L&-L)というのは、左端がLかつ自身が右の子であるようなノードのインデックスです。
[https://komiyam.hatenadiary.org/entry/20131202/1385992406](https://komiyam.hatenadiary.org/entry/20131202/1385992406)
