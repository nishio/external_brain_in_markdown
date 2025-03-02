---
title: "heapq"
---

[[二分ヒープ]]のPython標準ライブラリ
- 値を追加し、最小値を取得、削除できる[[データ構造]]

任意の値の削除はできないが、読み飛ばす技法で応用範囲が広がる。

[heapq --- ヒープキューアルゴリズム — Python 3.8.3 ドキュメント](https://docs.python.org/ja/3/library/heapq.html)
[[ヒープキュー]] [[優先度キュー]] [[Priority Queue]]
[https://github.com/python/cpython/blob/master/Lib/heapq.py](https://github.com/python/cpython/blob/master/Lib/heapq.py)

技法
- [[ある集合に値が追加削除される。最小の値を取得したい。]]
- [[M個の数がN個の集合を移動する。集合の最小要素を得たい]]
- [[N個の値が更新される、最小値を知りたい]]
- [[ヒープのK番目の値を更新したい]]
- [[中央値]]
- [[Best Kの取得]]