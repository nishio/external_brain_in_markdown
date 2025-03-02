---
title: "Evolutionary Optimization of Model Merging Recipes"
---

[Evolutionary Optimization of Model Merging Recipes](https://arxiv.org/abs/2403.13187)

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>この論文は、[[進化的アルゴリズム]]を用いてモデルマージのレシピを最適化する新しいアプローチを提案しています。主なポイントは以下の通りです:

- モデルマージは異なる専門性を持つモデルを組み合わせて新しい強力なモデルを作る有望なアプローチだが、現状は人間の直感と専門知識に頼っている。進化的手法ならこれを自動化できる可能性がある。
- パラメータ空間とデータフロー空間の両方でモデルマージを最適化する統合的なフレームワークを提案。これにより、モデルの重みだけでなく推論経路も同時に最適化できる。
- 異分野のモデル(例:日本語LLMと数学推論モデル)をマージして、日本語で数学問題が解けるモデルなどを自動生成することに成功。驚くべきことに、明示的に最適化していないタスクでもSOTAを達成。
- 日本の文化に特化したコンテンツを適切に扱える日本語VLMの自動生成にも成功。従来の日本語VLMを上回る性能を実証。
この手法で生成したモデルをオープンソース化。また、ゼロから大規模なモデルを学習するのではなく、既存モデルを組み合わせて強力なモデルを効率的に作れる可能性を示した。

要するに、進化的アルゴリズムを用いてモデルマージのプロセスを自動化・最適化する新しいパラダイムを提示した挑戦的な研究と言えます。異分野のモデルを融合して新しい能力を引き出せる可能性を示した点が特に印象的です。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>"モデルの重みだけでなく推論経路も同時に最適化"とは？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>論文で提案されている進化的モデルマージの手法では、モデルを組み合わせる際の最適化を2つの異なる空間で行っています。

- パラメータ空間 (PS: Parameter Space) 各層のパラメータ(重み)をどのような比率で組み合わせるかを最適化します。つまり、ソースモデルの重みを混ぜ合わせる際の最適な混合比率を見つけ出します。
- データフロー空間 (DFS: Data Flow Space) モデルの推論時に、データ(トークン)がどのような経路を通るかを最適化します。具体的には、あるモデルのi番目の層を通った後、別のモデルのj番目の層に渡すといった具合に、推論時のデータの流れを決める層の接続を最適化します。

これら2つの空間でマージの設定を同時に最適化することで、単に重みを組み合わせるだけでなく、推論時のデータの流れまで考慮に入れてモデルを作ることができます。これにより、重みの混合比率と推論経路の両方が最適なモデルを見つけ出せるわけです。

このように、パラメータ空間とデータフロー空間の両方を探索することが、この手法の大きな特徴であり、強力な性能を生み出している要因の1つだと考えられます。単に重みを平均するだけの単純な手法に比べて、より柔軟にモデルを組み合わせることが可能になっているのです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>重みを混ぜ合わせる際の最適な混合比率はどのようにして見つける？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>論文では、重みの最適な混合比率を見つけるために、進化的アルゴリズムの1つである[[CMA-ES]] ([[Covariance Matrix Adaptation Evolution Strategy]]) を使用しています。

CMA-ESは、連続的な最適化問題を解くための強力な手法です。大まかな流れは以下の通りです:

- 初期化: mixing weightの初期値を設定します(例えば全て0.5)。また、探索の範囲を決めるハイパーパラメータ(共分散行列など)を初期化します。
- 評価: 現在のmixing weightを使ってモデルを組み合わせ、性能を評価します(例えば精度など)。この性能指標は適応度(fitness)と呼ばれます。
- 更新: 評価結果を基に、次の探索点を生成します。具体的には、適応度の高かった点の近傍を重点的に探索するように、共分散行列を更新します。
- 終了条件を満たすまで、2と3を繰り返します。

このように、CMA-ESでは評価と更新を繰り返しながら、最適なmixing weightを探索していきます。探索の際は、適応度の高い点の周辺を重点的に探索するため、効率的に最適解を見つけ出すことができます。

また、CMA-ESには理論的な裏付けがあり、非凸な問題にも適用できるため、ニューラルネットワークの最適化などでもよく使われています。

論文では、この手法を[[TIES-Merge]]や[[DARE]]といった既存のマージ手法と組み合わせることで、さらに性能を向上させています。CMA-ESによって最適なmixing weightを見つけ出し、その重みでモデルを組み合わせることで、タスクに適した強力なモデルを作り出しているわけです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>データフロー空間での最適化はどうやる？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>データフロー空間 (DFS) でのモデルマージの最適化は、推論時のデータの流れを決める層の接続を進化的アルゴリズムで探索することで行われます。論文では、以下のようなアプローチが取られています。

- 探索空間の定義: まず、層の接続を表現する探索空間を定義します。具体的には、「indicator array」と呼ばれる、層の使用/不使用を表すバイナリベクトルを導入します。例えば、`[1, 0, 1, 1, 0]` というベクトルは、1番目、3番目、4番目の層を使用することを表します。
- 探索空間の削減: 層の数をM、繰り返し回数をrとすると、可能な層の接続パターンは2^(M*r)通りになります。これは膨大な数になるため、経験的に良くなさそうなパターン(例えば、同じ層を連続で使うなど)を排除することで、探索空間を削減します。
- 重み行列の導入: 異なるモデルの層を接続する際、入力の分布が変わることで性能が低下する可能性があります。これを緩和するため、層間の接続に重み行列を導入します。この重み行列も進化的アルゴリズムで最適化します。
- 進化的探索の実行: indicator arrayと重み行列を合わせて個体とみなし、進化的アルゴリズム(論文ではCMA-ESを使用)で最適な値を探索します。評価指標としては、validation setでの性能を使用します。
- 最良個体の選択: 探索終了後、最もvalidation setでの性能が高かった個体を最終的なモデルとして選択します。

このようなプロセスを経て、データフロー空間での最適なモデルマージを実現しています。重要なのは、層の接続を直接探索空間に組み込んでいる点です。これにより、ソースモデルの層を柔軟に組み合わせ、タスクに適した推論経路を見つけ出すことができます。

また、異なるモデル間の層の接続に重み行列を導入している点も特徴的です。これにより、単純に層を接続するだけでなく、データの分布の違いを吸収することができ、性能の低下を防ぐことができます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>"推論時のデータの流れ"という言葉の意味がよくわからない

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>はい、「推論時のデータの流れ」というのは少しわかりにくい表現かもしれません。ニューラルネットワークの文脈で言い換えると、「入力データが推論の際にたどるニューラルネットワークの層の順序」といえます。

ニューラルネットワークは通常、複数の層を順番に接続して構成されています。例えば、入力層、中間層1、中間層2、出力層、といった具合です。通常、入力データは入力層から順番に各層を通過し、最終的に出力層から結果が出力されます。

しかし、この論文で提案されているデータフロー空間でのモデルマージでは、この層の接続順序を変更することを考えています。例えば、モデルAの入力層と中間層1を使った後、モデルBの中間層2に接続する、といったように、異なるモデルの層を組み合わせて新しいネットワーク構造を作ります。

この新しいネットワーク構造では、データが通る層の順序が元のモデルとは異なります。つまり、「推論時のデータの流れ」が変わるわけです。

論文ではこの層の接続方法、すなわち「推論時のデータの流れ」を進化的アルゴリズムで最適化することで、タスクに適したネットワーク構造を見つけ出そうとしているのです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>"層の接続順序を変更する" ええっ、そうなのですか、これは一般的なことですか？論文のどこに書いてますか？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>ご指摘ありがとうございます。層の接続順序を変更するというのは、一般的なニューラルネットワークの学習方法ではありません。私の説明が不十分でしたね。

この論文で提案されている手法は、異なるモデルの層を組み合わせて新しいネットワーク構造を作るという点で、通常のニューラルネットワークの学習とは異なるアプローチです。

論文の "3.2 Merging in the Data Flow Space" の部分に、この点について以下のように書かれています:

> In our initial effort in this domain, we limit ourselves to serial connections and non-adaptive configurations, deferring the investigation of more flexible model merging to future work. Concretely, with a collection of N models and a budget T, our method searches for a sequence of layer indices L(t)i,j that delineates the path all the tokens should follow for a specific task. Here Li,j denotes the j-th layer in the i-th model, with t ∈ `[1, T]` marking the step in the inference path.

つまり、N個のモデルの層を組み合わせて、T個の層からなる新しいネットワーク構造を作ることを考えています。この新しいネットワークでは、データはL(t)i,jで指定された順番で層を通過します。

また、"3.2 Merging in the Data Flow Space" の最後の方には、以下のような記述もあります:

> In this setting, a layer may face an input whose distribution is different from what it is used to (from its original model), leading to unexpected outputs. For example, our preliminary studies show that swapping a pair of neighboring layers in a language model makes its performance drop. Although more theoretical studies are needed to model the distribution shift, empirically we find that appropriately scaling an input that wishes to go from layer i to j by Wij help alleviate the problem.

ここでは、異なるモデルの層を接続する際に、入力の分布が変化することで性能が低下する可能性について言及されています。

このように、この論文では、異なるモデルの層を組み合わせて推論経路を最適化するという、一般的ではないアプローチが提案されています。私は当初、この点をわかりやすく説明しようとするあまり、不正確な表現を用いてしまいました。お詫び申し上げます。

(ここで論文を読む)
- AIが引用したののひとつ前の段落で「モデルAのi層を使った後、モデルBのj層に接続する」という例を説明してるな
- > Recent analysis and discoveries imply that knowledge is stored distributedly in language models `[14, 35, 36]`, suggesting simple yet novel model merging possibilities in the data flow space (DFS). Unlike merging in PS, model merging in DFS preserves the original weights of each layer intact. Instead, it optimizes the inference path that tokens follow as they traverse through the neural network. For example, after the i-th layer in model A, a token may be directed to the j-th layer in model B.
