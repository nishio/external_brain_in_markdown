---
title: "ACLPC K"
---

from [[AtCoder Library Practice Contest]]
ACLPC_K
[K - Range Affine Range Sum](https://atcoder.jp/contests/practice2/tasks/practice2_k)
- ![image](https://gyazo.com/5b8f41c3ba45a6f2bcaeb91a7353f862/thumb/1000)
- 範囲更新範囲縮約なので[[遅延セグメント木]]
- 最初、作用をタプルで持っててTLE
- 32ビットシフトして一つの整数に束ねるようにしてAC
- シフト演算子の優先順序とか、Cの剰余取ってなくて32ビットをはみ出したりとかでバグらせた
