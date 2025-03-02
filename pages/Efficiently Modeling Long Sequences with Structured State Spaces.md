---
title: "Efficiently Modeling Long Sequences with Structured State Spaces"
---

[https://arxiv.org/abs/2111.00396](https://arxiv.org/abs/2111.00396)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文は、[[長期的依存関係]]のあるシーケンスを効率的にモデル化するための新しいモデルS4 (Structured State Space)を提案しています。主なポイントは以下の通りです。
- S4は、[[状態空間モデル]](SSM)をベースに、連続時間、畳み込み、再帰表現を組み合わせたモデル。これにより長期的依存関係を理論的かつ経験的に捉えられる。
- 計算効率のため、状態行列Aを正規行列と低ランク行列の和で再パラメータ化。これにより対角化と高速計算が可能に。
- 理論的にはO(N+L)の計算量と空間量で動作。Nは状態サイズ、Lはシーケンス長。
- 様々なベンチマークで従来手法を大きく上回る性能。画像分類、言語モデル、時系列予測など幅広いタスクで汎用的に適用可能。
- 特に16,384ステップの超長シーケンスからなるLong Range Arenaにおいて、平均86%の高精度。
- 大規模生成タスクでもTransformerに迫る高性能と60倍の高速生成を実現。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>状態空間モデルとは

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>状態空間モデル(State Space Model; SSM)は、時系列データをモデル化するための確率的なフレームワークです。主に制御理論や時系列解析の分野で使われてきましたが、近年は機械学習、特に深層学習においても注目されています。

SSMでは、観測可能な変数(observation)と、直接観測できない隠れ変数(latent variable or hidden state)の2種類の変数を考えます。隠れ変数は、システムの内部状態を表現し、その時間的な遷移により観測変数の生成過程をモデル化します。
(数式略)
SSMの利点は、システムのダイナミクスを明示的にモデル化できること、状態推定やパラメータ推定のための統計的な手法が豊富に存在すること、制御理論との親和性が高いことなどが挙げられます。

近年の深層学習では、RNNの一般化としてSSMを用いる試みや、SSMを深層ニューラルネットワークと組み合わせる研究が盛んに行われています。本論文のS4もそうした流れに位置づけられます。SSMの枠組みを用いることで、長期依存性のモデル化や計算効率の改善を目指しているわけです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>S4は何の改善？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>S4 (Structured State Space Sequence model) は、以下の点で既存のモデルを改善しています。

- 長期依存性 (Long-range dependencies) のモデル化: S4は、状態空間モデルの枠組みを用いることで、長いシーケンスにおける長期的な依存関係を効果的に捉えることができます。特に、HiPPO (High-order Polynomial Projection Operator) という理論に基づいて状態行列Aを設計することで、長期記憶を実現しています。
- 計算効率の改善: 従来の状態空間モデルは計算量が大きく、長いシーケンスを扱うことが難しいという問題がありました。S4はこれを解決するために、状態行列Aを正規行列と低ランク行列の和 (Normal Plus Low-Rank; NPLR) で表現し、効率的な計算アルゴリズムを導入しています。これにより、シーケンス長Lと状態の次元Nに対して、O(L+N)の計算量を達成しています。
- Transformerの代替モデルとしての可能性: S4は、RNNやCNNだけでなく、Transformerに代わる新しいシーケンスモデルとしての可能性を示しました。LayerNormやResidual connectionなどを組み合わせることで、画像分類、言語モデル、時系列予測など、様々なタスクでTransformerに匹敵する、あるいはそれを上回る性能を達成しています。
- 理論と実践の両立: S4は、HiPPOのような数学的な原理に基づきながらも、大規模な実験によってその有効性を実証しています。理論的な裏付けがあることで、モデルの振る舞いが解釈しやすく、さらなる改良の指針が得られます。

全体として、S4は状態空間モデルの枠組みを用いて、長期依存性のモデル化と計算効率の改善を両立し、Transformerに代わる新しいシーケンスモデルの可能性を示した画期的な研究だと言えます。理論と実践のバランスの取れたアプローチは、今後のシーケンスモデリング研究に大きな影響を与えるでしょう。

