---
title: "ヒープのK番目の値を更新したい"
---

from [[heapq]]
ヒープのK番目の値を更新したい。
→書き換えてから_siftdownでO(logN)でヒープの状態に戻せる
- ただしこのKはソート順でのK番目ではないので使い勝手が悪い。任意の値を更新したい場合にはその値がどこに入ってるのかを見つけるのにO(N)掛かってしまう
    - see [[heapq+dict]]
- 例えば「2番目に大きい値を更新」とかならK=1,2の2箇所の比較で決まるので使えなくもないかな？という感じ
python

```
from heapq import _siftdown

queue = [1, 2, 3]
K = 1
queue[K] = -1
_siftdown(queue, 0, K)
print(queue)  # => [-1, 1, 3]
```

