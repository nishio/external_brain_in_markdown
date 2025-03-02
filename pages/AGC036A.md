---
title: "AGC036A"
---

[A - Triangle](https://atcoder.jp/contests/agc036/tasks/agc036_a)
- ![image](https://gyazo.com/00c2a55af4f2c2390acec060dac38f9c/thumb/1000)

- 考えたこと
    - まず要求されてる最大の三角形を考えて、次にそこから1小さい三角形を考えた
    - ![image](https://gyazo.com/0c706bc7c10cbf0775ba87d6ea6b2def/thumb/1000)
    - 一般化すると(0, 0), (1, 10^9), (10^9, i) for 0 <= i <= 10^9 で 10^18-i が表現できる
    - それよりさらに小さいものは？
        - (0, 0), (1, 10^9 - j), (10^9, i) で 10^18 - j * 10^9 - i が表現できる
- 公式解説
    - まったく同じ
