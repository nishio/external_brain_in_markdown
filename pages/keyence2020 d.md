---
title: "keyence2020 d"
---

from [[競技プログラミングで解法を思いつくための典型的な考え方]]
keyence2020_d
[https://atcoder.jp/contests/keyence2020/tasks/keyence2020_d](https://atcoder.jp/contests/keyence2020/tasks/keyence2020_d)
- 考えたこと
    - N=18
    - 操作は無限に繰り返せるので、まず「操作を繰り返すことで到達可能な集合」を考える？
        - 必要最小回数も要求されてるから微妙？
    - 互換を繰り返して任意の順番にできる
    - 元の位置から奇数離れてる場合には裏返る
    - 2^18は10^6よりは小さいな、18掛けても計算可能な範囲かな
        - いや順列だから18!か、それは無理そう
    - 1枚目と2枚目が決まった時点で制約を満たしてなかったら以降で満たすことはない
        - でもこれで枝刈りしながら探索するのは、全てが同じ値であるようなケースで全探索になるから無理だな
        - こういうケースは最小値を求めるとすぐ求まりそう
- 公式解説
    - [[bit DP]]
    - 具体的なことがよくわからない
- [https://www.hamayanhamayan.com/entry/2020/01/18/233933](https://www.hamayanhamayan.com/entry/2020/01/18/233933)
    - > 既に整列済みの集合がmskで、最後の値がlstであるときの操作の最小値
    - 使用済みの値の集合は2^Nなのでこれをbitで表現する
    - それだけでは「単調増加」を保ちながら追加できるかわからないので、最後のカードも保持する
    - O(N 2^N)

![image](https://gyazo.com/227ef044f17cd3088465d5c3121bc561/thumb/1000)
- 境界部分より手前に関して[[操作の順序は関係ない]]ことを使う
