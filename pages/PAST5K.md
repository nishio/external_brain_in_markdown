---
title: "PAST5K"
---

[K - 的あて](https://atcoder.jp/contests/past202012-open/tasks/past202012_k)
![image](https://gyazo.com/6479e86b1c951eb67508032cd297072f/thumb/1000)
- 初回考察
    - 残っている的が2^16
    - 定義域が集合の部分集合なので[[bit DP]]する
    - 期待値を値域とする[[期待値DP]]
        - 先の左右に同じ項がでてくるので整理して消去する必要がある。
    - 考察完了
