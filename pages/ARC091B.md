---
title: "ARC091B"
---

[D - Remainder Reminder](https://atcoder.jp/contests/arc091/tasks/arc091_b)
- ![image](https://gyazo.com/fcef21e76d5fe9ebcd49ecfe88f6fad6/thumb/1000)
- 考えたこと
    - 条件を満たす数を素朴に探すと10^10でダメ
    - 各bごとに計算
        - kより小さいなら0
        - 大きいならNをbで割る→q, r
        - ret = q * (b - k)
        - r > k なら ret += r - k
- 公式解説OK
    - 1つズレてるけどテストケースですぐ直せるでしょう

[[ARC091]]
[[ARC]]
