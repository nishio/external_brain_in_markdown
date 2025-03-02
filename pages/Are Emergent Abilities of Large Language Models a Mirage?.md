---
title: "Are Emergent Abilities of Large Language Models a Mirage?"
---

LLMが「規模の拡大に伴って急激に賢くなる」ように見えるのは、単に賢さの尺度に正解率のような非線形の尺度を使っているからそう見えているだけで、トークン編集距離のような尺度を使えば急激に賢くはなってないことがわかる、という主張
![image](https://gyazo.com/405cb26843247336fa3ee4b9046fecfa/thumb/1000)
- (DeepL) 主張される創発的な能力は、指標を変えると蒸発する。左から右へ： 数学モデル、2整数2桁の掛け算課題、2整数4桁の足し算課題。上：非線形の測定基準（例えば、正確さ）で性能を測定した場合、InstructGPT/GPT-3 ファミリーの性能は、より長いターゲット長で鋭く、予測不可能に見える。下図： 代わりに線形指標（例：トークン編集距離）で性能を測定すると、ファミリーはスムーズで予測可能な性能向上を示す。

西尾の補足
- ![image](https://gyazo.com/430921b29980726eee4ac1f7760031c8/thumb/1000)
- 正解率を尺度にすると「閾値を超えたら100点、超えなければ0点」という閾値関数を掛けることになる
- たとえ同じ形の分布の平均値が滑らかに上昇しているような状況でも、その閾値関数を通すことで性能のグラフには分布の微分の形状が現れる
- 分布が釣鐘型なら微分はS字カーブになる
- なので性能のグラフに急速な立ち上がりがあったとしても、それは非線形な尺度の性質から生まれている可能性がある

> Recent work claims that large language models display emergent abilities, abilities not present in smaller-scale models that are present in larger-scale models. What makes emergent abilities intriguing is two-fold: their sharpness, transitioning seemingly instantaneously from not present to present, and their unpredictability, appearing at seemingly unforeseeable model scales. Here, we present an alternative explanation for emergent abilities: that for a particular task and model family, when analyzing fixed model outputs, emergent abilities appear due to the researcher's choice of metric rather than due to fundamental changes in model behavior with scale. Specifically, nonlinear or discontinuous metrics produce apparent emergent abilities, whereas linear or continuous metrics produce smooth, continuous predictable changes in model performance. We present our alternative explanation in a simple mathematical model, then test it in three complementary ways: we (1) make, test and confirm three predictions on the effect of metric choice using the InstructGPT/GPT-3 family on tasks with claimed emergent abilities; (2) make, test and confirm two predictions about metric choices in a meta-analysis of emergent abilities on BIG-Bench; and (3) show to choose metrics to produce never-before-seen seemingly emergent abilities in multiple vision tasks across diverse deep networks. Via all three analyses, we provide evidence that alleged emergent abilities evaporate with different metrics or with better statistics, and may not be a fundamental property of scaling AI models.
[https://arxiv.org/abs/2304.15004](https://arxiv.org/abs/2304.15004)
(DeepL)最近の研究では、大規模な言語モデルは、より小規模なモデルには存在しない能力が、より大規模なモデルには存在するという、創発的な能力を示すと主張されている。創発的能力の興味深い点は2つある。1つは、存在しない状態から存在する状態へと瞬時に移行する鋭さ、もう1つは、一見予測不可能なモデルスケールで現れる予測不可能性である。すなわち、特定のタスクとモデルファミリーについて、固定されたモデル出力を分析するとき、スケールによるモデル動作の基本的な変化によるのではなく、研究者のメトリックの選択によって、出現能力が現れるということである。具体的には、非線形または不連続なメトリクスは、見かけ上の創発的能力を生み出すが、線形または連続的なメトリクスは、モデル性能の滑らかで連続的な予測可能な変化を生み出す。(1)InstructGPT/GPT-3ファミリーを用いて、創発能力が主張されるタスクにおけるメトリック選択の効果について3つの予測を行い、テストし、確認する。(2)BIG-Benchにおける創発能力のメタ分析において、メトリック選択に関する2つの予測を行い、テストし、確認する。3つの分析を通して、我々は、主張される創発的な能力は、異なるメトリクスや、より優れた統計によって蒸発し、スケーリングAIモデルの基本的な特性ではない可能性があるという証拠を提供する。
