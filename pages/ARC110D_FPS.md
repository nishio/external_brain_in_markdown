---
title: "ARC110D_FPS"
---

![image](https://gyazo.com/829c06c94c53cc49c05c234e5f3445c5/thumb/1000)
[D - Binomial Coefficient is Fun](https://atcoder.jp/contests/arc110/tasks/arc110_d)

[[ARC110D]]を[[形式的べき級数]]に帰着して解く

$F_{i}(x) = \sum_{k=0}^{\infty} \binom{k}{A_{i}} x^{k}$
$ G(x) = \prod_{i=1}^{N} F_{i}(x)$
- [[下固定の二項係数→負の二項定理]]:
    - $\binom{A+i}{A} = [x^i] \sum_n \binom{A+n}{A}x^n = [x^i]\frac{1}{(1-x)^{A+1}} $
- $i < 0$の時 $\binom{A+i}{A} = 0$ であることから $F_{i}(x) = \sum_{k=0}^{\infty} \binom{k}{A_{i}} x^{k} = \frac{x^{A_i}}{(1-x)^{A_i+1}}$

$S := \sum A_i$

$ G(x) = \prod_{i=1}^{N} F_{i}(x) = \frac{x^S}{(1-x)^{S+N}}$

- [[形式的べき級数の係数の部分和]]:
- $\displaystyle \sum_{i=0}^{k} [x^{i}]F =  [x^{k}] \frac{1}{1-x}F$

$X = \sum_{i=}^{M} [x^{i}]G =  [x^{M}] \frac{1}{1-x}G = [x^{M}]\frac{x^S}{(1-x)^{S+N+1}}$
$= [x^{M-S}]\frac{1}{(1-x)^{S+N+1}}$

- [[べき級数→二項係数]]:
    - $[x^B]\frac{1}{(1-x)^{A}} = \binom{A+B-1}{A-1}$

$[x^{M-S}]\frac{1}{(1-x)^{S+N+1}} = \binom{S+N+1+M-S-1}{S+N} = \binom{N+M}{S+N}$


参考
- [https://maspypy.com/atcoder-参加感想-2020-12-06arc110](https://maspypy.com/atcoder-参加感想-2020-12-06arc110)
    - ほぼこれの流れ
- [https://twitter.com/kyopro_friends/status/1335227103797673984?s=21](https://twitter.com/kyopro_friends/status/1335227103797673984?s=21)
- [https://twitter.com/maspy_stars/status/1335225085255319556?s=21](https://twitter.com/maspy_stars/status/1335225085255319556?s=21)
- [https://scol.hatenablog.com/entry/2020/12/06/015509](https://scol.hatenablog.com/entry/2020/12/06/015509)
