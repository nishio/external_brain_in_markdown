---
title: "DSL 2 D Range Update Query"
---

from [[セグメント木の可視化]]
DSL_2_D Range Update Query
- [DSL_2_D Range Update Query](https://onlinejudge.u-aizu.ac.jp/courses/library/3/DSL/2/DSL_2_D)
    - 「値を上書きする」の範囲作用がどう定義されるべきか
    - 範囲作用はノードが上にあるか下にあるかでどちらが後かわからない
    - そこで値をタイムスタンプ付きにして、下への伝搬は「タイムスタンプの新しい方を取る」二項演算にした
    - 別解 [[双対セグメント木の下への伝搬]]
python

```
def main():
    N, Q = map(int, input().split())
    depth = N.bit_length() + 1
    set_depth(depth)
    action_unity = (-1, INF)
    table = [action_unity] * SEGTREE_SIZE

    for time in range(Q):
        q, *args = map(int, input().split())
        if q == 0:
            # update
            s, t, new_value = args
            range_update(table, s, t + 1, lambda x: (time, new_value))

        else:
            # find
            print(down_propagate_to_leaf(
                table, args[0], max, action_unity)[1])
```

