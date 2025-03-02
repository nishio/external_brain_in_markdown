---
title: "eq7-proof"
---

from [[二項係数の公式]]
- eq7-proof
    - $[x^k]F = \sum_{i=0}^k \binom{n+1}{i}\binom{m-i}{k - i}$であるような形式的べき級数Fを考える
    - $\displaystyle F = \sum _ {k=0}^{\infty} \sum_{i=0}^{k} {n+i \choose i}{m-i \choose k-i} x^{k}$
    - $k < i$の時$\binom{m-i}{k-i} = 0$ なので $\sum_{i=0}^{k}$を $\sum_{i=0}^{\infty}$ にして良い
    - $\displaystyle F = \sum _ {k=0}^{\infty} \sum _ {i=0}^{\infty} {n+i \choose i}{m-i \choose k-i} x^{k}$
    - $\displaystyle F = \sum_{i=0}^{\infty} \sum_{k=0}^{\infty} {n+i \choose i}{m-i \choose k-i} x^{k}$ ... [[足し算の順序の変更]]
    - $\displaystyle F = \sum_{i=0}^{\infty}\left({n+i \choose i} \sum_{k=0}^{\infty} {m-i \choose k-i} x^{k}\right)$ ... kに依存しない係数をくくりだし
    - $k < i$の時$\binom{m-i}{k-i} = 0$ なので$j=k - i \quad (j > 0)$として
    - $\displaystyle F = \sum_{i=0}^{\infty}\left({n+i \choose i} \sum_{j=0}^{\infty} {m-i \choose j} x^{j}x^i\right)$

    - $\displaystyle F = \sum_{i=0}^{\infty}\left({n+i \choose i} (1+x)^{m-i} x^i\right)$ ... [[二項定理]]

    - $\displaystyle F = \sum_{i=0}^{\infty}\left({n+i \choose i} (1+x)^m(1+x)^{-i} x^i\right)$
    - $\displaystyle F = (1+x)^m \sum_{i=0}^{\infty}\left({n+i \choose i} \left(\frac{x}{1+x}\right)^i \right)$ ... iに依存しない係数をくくりだし
    - $\displaystyle F = (1+x)^m \sum_{i=0}^{\infty}\left({i+n \choose n} \left(\frac{x}{1+x}\right)^i \right)$ ... by eq4-3
    - $\displaystyle F = (1+x)^m / \left(1 - \frac{x}{1+x}\right)^{n+1} $ ... [[負の二項定理]]
    - $\displaystyle F = (1+x)^m / \left(\frac{1}{1+x}\right)^{n+1} $

    - $\displaystyle F = (1+x)^m (1+x)^{n+1} $

    - $\displaystyle F = (1+x)^{m+n+1} $
    - $\displaystyle F = \sum_{k=0}^\infty \binom{m+n+1}{k} x^k$... [[二項定理]]
    - $[x^k]F = \binom{m+n+1}{k}$
