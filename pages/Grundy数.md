---
title: "Grundy数"
---

- 負け状態のGrundy数は0
- ある状態のGrundy数はそこから遷移可能な状態のGrundy数以外の最小の非負整数
    - mex: minimum excluded value

- [[Nim]]の一山の石の数がGrundy数と一致する

- なぜXORして良いのか？
    - 各山のGrundy数をgiとする
    - xorで結合したものをgとする
    - $g = \bigoplus_i g_i$
    - このgがGrundy数の条件を満たすことが証明できるから
    - やりかけ証明
        - gの最上位ビットをmとする。mをもつgiが必ず奇数個存在する。その一つをg1とする
        - $g_1 \& m = m$
        - $g_1 \oplus g < g_1$であるので遷移可能
        - $\left( \bigoplus_i g_i [i \neq 1] \right) \oplus (g_1 \oplus g) = \left(g_1 \oplus \bigoplus_i g_i [i \neq 1] \right) \oplus g = \left( \bigoplus_i g_i \right) \oplus g = g \oplus g = 0$
        - see [Grundy数（Nim数, Nimber）の理論](https://www.creativ.xyz/grundy-number-1065/)
