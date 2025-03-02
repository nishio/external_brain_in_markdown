---
title: "Information-Geometric Optimization"
---

2019-07-29
探索空間で定義された目的関数をパラメータ空間で定義された関数に変換する際に、従来は一般的に期待値を取る方法が使われれいたが、[[平均は目的関数の単調増加な関数による写像に対して不変量ではない]]のでquantileを用いた定義に変えた
- 勉強会発表資料: [[Information-Geometric Optimizationの紹介]]

![image](https://gyazo.com/0a5fbd0a8c79402a155318bd154447b5/thumb/1000)

[http://www.jmlr.org/papers/volume18/14-467/14-467.pdf](http://www.jmlr.org/papers/volume18/14-467/14-467.pdf)
- We present a canonical way to turn any smooth parametric family of probability distributions on an arbitrary search space 𝑋 into a continuous-time black-box optimization method on 𝑋, the [[information-geometric optimization]] ([[IGO]]) method.
- [[Invariance]] as a major design principle keeps the number of arbitrary choices to a minimum.
- The resulting [[IGO flow]] is the flow of an ordinary differential equation conducting the [[natural gradient ascent]] of an adaptive, time-dependent transformation of the objective function.
- It makes no particular assumptions on the objective function to be optimized.
- The IGO method produces explicit [[IGO algorithms]] through time discretization.
- It naturally recovers versions of known algorithms and offers a systematic way to derive new ones.
    - In continuous search spaces, IGO algorithms take a form related to [[natural evolution strategies]] ([[NES]]).
    - The [[cross-entropy method]] is recovered in a particular case with a large time step, and can be extended into a smoothed, parametrization-independent maximum likelihood update (IGO-ML).
    - When applied to the family of Gaussian distributions on $R^d$, the IGO framework recovers a version of the well-known [[CMA-ES]] algorithm and of [[xNES]].
    - For the family of [[Bernoulli distributions]] on $\{0, 1\}^d$, we recover the [[seminal PBIL]] algorithm and [[cGA]].
    - For the distributions of restricted Boltzmann machines, we naturally obtain a novel algorithm for discrete optimization on $\{0, 1\}^d$.
- All these algorithms are natural instances of, and unified under, the single information-geometric optimization framework.
- The IGO method achieves, thanks to its intrinsic formulation, maximal invariance properties:
    - invariance under reparametrization of the search space 𝑋,
    - under a change of parameters of the probability distribution,
    - and under increasing transformation of the function to be optimized.
    - The latter is achieved through an adaptive, quantile-based formulation of the objective.
- Theoretical considerations strongly suggest that IGO algorithms are essentially characterized by a minimal change of the distribution over time. Therefore they have minimal loss in diversity through the course of optimization, provided the initial diversity is high. First experiments using restricted Boltzmann machines confirm this insight. As a simple consequence, IGO seems to provide, from information theory, an elegant way to simultaneously explore several valleys of a fitness landscape in a single run.

- search space: X
    - 有限、離散無限、連続のどれでもあり得る
- objective function$f: X \to R$
- black-box senario: f(x)を求める以外のfに関する知識は得られないものとする
- invariance
    - extends performance observed on a single function to an entire associated invariance class
    - generalizes from a single problem to a class of problems
    - ??
    - Thus it hopefully provides better robustness w.r.t. changes in the presentation of a problem.
- For continuous search spaces, invariance under translation of the coordinate system is standard in optimization.
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>あー、不変量の概念か
- Invariance under general affine-linear changes of the coordinates has been
    - Nelder-Mead Downhill Simplex method (Nelder and Mead, 1965),
    - quasi-Newton methods (Deuflhard, 2011)
    - [[covariance matrix adaptation evolution strategy]], [[CMA-ES]] (Hansen and Ostermeier, 2001; Hansen and Auger, 2014)
- これらは探索空間に対する不変量
- 一方、目的関数に対する単調増加な変換

- iteratively update a probability distribution $𝑃_\theta$ defined on 𝑋, parametrized by a set of parameters $\theta$
    - この確率分布は解に対する[[信念]]と言える([[POMDP]]などでの意味の)

- [[estimation of distribution algorithms]] ([[EDA]])
    - 方法1: cross-entropy method consists in taking 𝜃 minimizing the Kullback–Leibler divergence between 𝑃𝜃 and the indicator of the best points according to 𝑓
        - indicator of the best points according to f とは？
    - 方法2: one can transfer the objective function 𝑓 to the space of parameters 𝜃 by taking the average of 𝑓 under 𝑃𝜃, seen as a function of 𝜃.
        - This average is a new function from an Euclidian space to R and is minimal when 𝑃𝜃 is concentrated on minima of 𝑓.
            - θは1次元という想定かな？
            - そうでなくても勾配法で解けるよね
    - 甘利の自然勾配法の話
        - 普通の勾配より効率的
- Euler time discretization
    - オイラー法
    - ルンゲクッタの手前

- 多分(1)の付いている場所、1つずれてる

- 2.2.1
    - fをXではなくthetaの上の関数にするにはthetaで期待値を取るのが手
    - だが
        - 期待値は極端な値に影響を受けやすい
        - 単調増加な変換に対して不変量ではない
    - だから百分量を使う
        - 中央値は単調増加な関数で変換しても中央値だからね
