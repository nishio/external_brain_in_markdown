---
title: "KL距離からのFisher行列の導出"
---


- [[Kullback-Leibler divergence]]([[KL距離]])の定義:
- $D(P, Q) = \int_\Omega P(\omega)\log{P(\omega) \over Q(\omega)} d \omega$
- 対称化すると:
- $D'(P, Q) \equiv D(p, Q) + D(Q, P)$
- $= \int_\Omega P(\omega)\log{P(\omega) \over Q(\omega)} + Q(\omega)\log{Q(\omega) \over P(\omega)} d \omega$
- $= \int_\Omega (P(\omega) - Q(\omega))\log{P(\omega) \over Q(\omega)} d \omega$

- あるパラメータθとちょっと(δ)ずれたパラメータの確率分布のKL距離:
- $D'(P(\omega| \theta+\delta), P(\omega|\theta)$
- $= \int_\Omega (P(\omega| \theta+\delta) - P(\omega| \theta))\log{P(\omega| \theta+\delta) \over P(\omega| \theta)} d \omega$
- ここで$\Delta \equiv P(\omega| \theta+\delta) - P(\omega| \theta)$ と置くと
- $= \int_\Omega \Delta \log{P(\omega| \theta) + \Delta  \over P(\omega| \theta)} d \omega$
- $= \int_\Omega \Delta \log \left( 1 + {\Delta  \over P(\omega| \theta)} \right) d \omega$
- 対数の[[テイラー展開]]と一次近似により
- $\log(1 + x) \approx x$
- なので
    - $\int_\Omega \Delta \log \left( 1 + {\Delta  \over P(\omega| \theta)} \right) d \omega \approx \int_\Omega { \Delta^2  \over P(\omega| \theta)}  d \omega$

- 関数の値の差の一次近似:
- $f(x+dx)-f(x) \approx f'(x)dx$
- によって
- $\Delta \equiv P(\omega| \theta+\delta) - P(\omega| \theta) \approx \sum_i {\partial P(\omega | \theta) \over \partial \theta_i} \delta_i$
- 対数の微分 $(\log x)' = x' / x$ により
- $= P(\omega|\theta) \sum_i {\partial \log P(\omega | \theta) \over \partial \theta_i} \delta_i$
- Δを代入すると:
    - $\int_\Omega { \Delta^2  \over P(\omega| \theta)}  d \omega   \approx   \int_\Omega \left( \sum_i {\partial \log P(\omega | \theta) \over \partial \theta_i} \delta_i \right)^2 P(\omega | \theta) d\omega$

整理すると:
- $\int_\Omega \left( \sum_i {\partial \log P(\omega | \theta) \over \partial \theta_i} \delta_i \right)^2 P(\omega | \theta) d\omega$
- $= {\mathbb E} \left[  \left( \sum_i {\partial \log P(\omega | \theta) \over \partial \theta_i} \delta_i \right)^2 \right]$
- $= \sum_i \sum_j {\mathbb E}\left[ {\partial \log P(\omega | \theta) \over \partial \theta_i} {\partial \log P(\omega | \theta) \over \partial \theta_j} \right]_{ij} \delta_i\delta_j$
- $= \sum_i \sum_j \mathcal{F}(\theta)_{ij} \delta_i \delta_j$

- ここまでをまとめると
    - $D'(P(\omega| \theta+\delta), P(\omega|\theta) \approx \sum_i \sum_j \mathcal{F}(\theta)_{ij} \delta_i \delta_j$
- つまりKL距離の入っている空間の[[計量テンソル]]は[[フィッシャー行列]]([[Fisher行列]])である
