---
title: "diverta2019_2_C"
---

[C - Successive Subtraction](https://atcoder.jp/contests/diverta2019-2/tasks/diverta2019_2_c)
- ![image](https://gyazo.com/b445456237ffb73c3e17a53ff8a93a4b/thumb/1000)

- 考えたこと
    - [[小さい方から順番に考える]]
    - 数が2個の時は大きい方から小さい方を引く
    - 3個の時は？
        - c-(a-b)は要するにc-a+b
    - つまりN/2個が負になる
    - じゃあソートして小さい方から半分を負にすればよい
- 公式解説
    - 3個の時に(a-b)-cを見落としてる

