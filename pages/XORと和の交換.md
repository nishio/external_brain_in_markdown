---
title: "XORと和の交換"
---

0/1の列に対して下記が成り立つ
- $\sum_i^N x_i = K \iff \sum_i^N (1 \oplus x_i) = N - K$

一般の整数列でも、ビットごとの列とみなせばいける [[足し算の順序の変更]] [[ABC147D]]
- $A_i = \sum_j x_{ij} 2^j$
