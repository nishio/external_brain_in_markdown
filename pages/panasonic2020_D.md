---
title: "panasonic2020_D"
---

[D - String Equivalence](https://atcoder.jp/contests/panasonic2020/tasks/panasonic2020_d)
- ![image](https://gyazo.com/a8b4b439b08c41341e3abcb3d0b259b3/thumb/1000)
- 考えたこと
    - 同じ文字である関係は推移的
        - だからN以下の整数の集合を1つ以上の集合に分割する方法を考えれば良い
    - 標準形の条件から、ある点で出現する数はそこまでで出現した数の最大値x+1以下である
        - さもなければその数をx+1に入れ替えたものの方が小さくて標準形の条件に矛盾する
    - というわけで各点でそれまでに出現した数+1までの選択肢を昇順で選ぶDFSで良さそう
- 公式解説OK
