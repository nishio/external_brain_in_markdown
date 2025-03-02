---
title: "ABC174D"
---

![image](https://gyazo.com/2b5229aa9bfb5bab165b982e0641755a/thumb/1000)
from [[ABC174]]
ABC174D
D - Alter Altar []](https://atcoder.jp/contests/abc174/tasks/abc174_d)
- ![image](https://gyazo.com/473d4f6d9bda62df85a8ed87e2d02976/thumb/1000)
- WRが含まれないようにしたいということは要するにR*W*にしたいということ
- 右端と左端から見ていって、ルールを破ってる石を交換すれば、ルールを守ってる範囲が単調に増加する
    - ![image](https://gyazo.com/2b5229aa9bfb5bab165b982e0641755a/thumb/1000)

    - 色替えは必要ない
    - 色替えが有効である場合、その対象石の交換でも同様に有効だから(雑)
        - ![image](https://gyazo.com/e3b8e85a6e2080078ea6e10bcd15fb5c/thumb/1000)
    - 少しまともな説明
        - 与えられた列を条件を満たすように並び替えたものを考える
        - 現在の列のその列との食い違いの個数をコストと呼ぶことにする
        - 上記の交換操作はコストを常に2減らす
        - 色変えはコストを1減らし、赤城の境界を1つ動かす
            - 境界が動いたことによって所属の変わった石が正しい色であればコストがさらに1下がるが、正しくない場合逆に1増える
        - よって色変えはコストを最大値2減らす。これは交換と同程度または劣った効率である。
python

```
def solve(N, CS):
    left = 0
    right = N - 1
    R = ord("R")
    W = ord("W")
    ret = 0
    while left < right:
        if CS[left] == R:
            left += 1
            continue
        if CS[right] == W:
            right -= 1
            continue
        # swap
        left += 1
        right -= 1
        ret += 1
    return ret
```

