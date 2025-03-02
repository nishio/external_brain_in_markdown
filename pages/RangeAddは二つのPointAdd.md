---
title: "RangeAddは二つのPointAdd"
---

[[Range Add Point Read]]は普通の[[セグメント木]]を使って2つのPoint AddとRange Sumで実現できる
- Readが頭から順番で良い場合はセグメント木を使わずとも単なる配列で良い
- 値の範囲が10^9とかだと配列では難しい。辞書を使うといい。see [[ABC188]]


- 目的とする配列自体ではなく隣接項目間の差分を持つ
    - [[累積和]]の逆変換
    - この概念に名前があった方がいいな、[[増分リスト]]と呼んでるのを見た
- Range Addは開始と終了でPoint Add
:

```
def RangeAdd(start, end, value):
	PointAdd(start, value)
	PointAdd(end, -value)
```

- Point Readはその位置までの、その位置を含む和
:

```
def PointRead(pos):
	RangeSum(0, pos + 1)
```


- ![image](https://gyazo.com/a7c5788e15c7b7e45cf475276b6d63b2/thumb/1000)

[[Range Add]]
