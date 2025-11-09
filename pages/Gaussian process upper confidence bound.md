---
title: "Gaussian process upper confidence bound"
---

[[GP-UCB]]
- まだ元論文を探したりはしてない
- [[ガウス過程回帰]]で不確実度を出せるのだから、当然[[UCB1]]アルゴリズムも使えるよね、という理解

[[Gaussian Process Optimization in the Bandit Setting: No Regret and Experimental Design]]
> Many applications require optimizing an unknown, noisy function that is expensive to evaluate. We formalize this task as a multi-armed bandit problem, where the payoff function is either sampled from a [[Gaussian process]] (GP) or has low RKHS norm. We resolve the important open problem of deriving regret bounds for this setting, which imply novel convergence rates for GP optimization. We analyze [[GP-UCB]], an intuitive upper-confidence based algorithm, and bound its cumulative regret in terms of maximal information gain, establishing a novel connection between GP optimization and experimental design. Moreover, by bounding the latter in terms of operator spectra, we obtain explicit sublinear regret bounds for many commonly used covariance functions. In some important cases, our bounds have surprisingly weak dependence on the dimensionality. In our experiments on real sensor data, GP-UCB compares favorably with other heuristical GP optimization approaches.
[https://arxiv.org/abs/0912.3995](https://arxiv.org/abs/0912.3995)

[[Randomized Gaussian Process Upper Confidence Bound with Tighter Bayesian Regret Bounds]]
> Gaussian process upper confidence bound ([[GP-UCB]]) is a theoretically promising approach for black-box optimization; however, the confidence parameter β is considerably large in the theorem and chosen heuristically in practice. Then, randomized GP-UCB (RGP-UCB) uses a randomized confidence parameter, which follows the Gamma distribution, to mitigate the impact of manually specifying β. This study first generalizes the regret analysis of RGP-UCB to a wider class of distributions, including the Gamma distribution. Furthermore, we propose improved RGP-UCB (IRGP-UCB) based on a two-parameter exponential distribution, which achieves tighter Bayesian regret bounds. IRGP-UCB does not require an increase in the confidence parameter in terms of the number of iterations, which avoids over-exploration in the later iterations. Finally, we demonstrate the effectiveness of IRGP-UCB through extensive experiments.
[https://arxiv.org/abs/2302.01511](https://arxiv.org/abs/2302.01511)
