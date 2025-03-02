---
title: "code_festival_2017_quala_C"
---

[C - Palindromic Matrix](https://atcoder.jp/contests/code-festival-2017-quala/tasks/code_festival_2017_quala_c)
- ![image](https://gyazo.com/c32e2bc86779703edecaefd6b7c69127/thumb/1000)

- 考えたこと
    - 実際に並び替えて確認などすると明らかに間に合わないのでなんらかの節約が必要
    - 横が奇数の時、中央以外の文字は全部偶数かある、偶数の時には全部の文字が偶数個ある
    - 存在するかどうかの判定だけなので頻度を数えて偶奇を見るだけで良いのでは
- 公式解説
    - 問題条件見落とし、縦にも回文になる
    - 縦が奇数か偶数かでも同様の場合わけをすると、1個、2個、4個必要な文字数がわかる。
