---
title: "ABC105C"
---

[C - Base -2 Number](https://atcoder.jp/contests/abc105/tasks/abc105_c)
- ![image](https://gyazo.com/138fd19d56e29837bebffb7acca1e9cf/thumb/1000)
- 考えたこと
    - [[小さい方から順番に考える]]
    - 1のとき1
    - 2のとき110
        - 4-2なので
    - 3のとき111
        - 2+1なので
    - 4のとき100
    - 5のとき101
    - 6のとき…
        - 11010
        - 4+2は8-2で、8が16-8だから
    - 奇数桁と偶数桁に分ける
        - [[偶奇に分けて集計]]
        - $N = S_0 \times (-2)^0 + S_1 \times (-2)^1 + ... + S_k \times (-2)^k$
        - $= \sum_{i \in (0,2,4,...)} S_i 2^i - \sum_{i \in (1, 3,...)} S_i 2^i$
        - $= S_0 + \sum_{i \in (2,4,...)} S_i 2^i - \sum_{i \in (1, 3,...)} S_i 2^i$

        - mod 4で第一項はS0, 第二項は0, 第三項は2S2
        - よって4で割った余によって下2桁が確定する
        - 残りを4で割れば同じことが繰り返せる
        - 0になるまで繰り返せばOK
        - 対数オーダー
- 公式解説
    - 同様に下から決めていく
