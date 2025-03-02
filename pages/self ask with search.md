---
title: "self ask with search"
---

[[self-ask]] [https://ofir.io/self-ask.pdf](https://ofir.io/self-ask.pdf)
MEASURING AND NARROWING THE COMPOSITIONALITY GAP IN LANGUAGE MODELS
- We investigate the ability of language models to perform compositional reasoning tasks where the overall solution depends on correctly composing the answers to sub-problems. We measure how often models can correctly answer all subproblems but not generate the overall solution, a ratio we call the compositionality gap. We evaluate this ratio by asking multi-hop questions with answers that require composing multiple facts unlikely to have been observed together during pretraining. In the GPT-3 family of models, as model size increases we show that the single-hop question answering performance improves faster than the multihop performance does, therefore the compositionality gap does not decrease. This surprising result suggests that while more powerful models memorize and recall more factual knowledge, they show no corresponding improvement in their ability to perform this kind of compositional reasoning.
- We then demonstrate how elicitive prompting (such as chain of thought) narrows the compositionality gap by reasoning explicitly instead of implicitly. We present a new method, self-ask, that further improves on chain of thought. In our method, the model explicitly asks itself (and then answers) follow-up questions before answering the initial question. We finally show that self-ask’s structured prompting lets us easily plug in a search engine to answer the follow-up questions, which additionally improves accuracy
(DeepL)
- 我々は、言語モデルによる構成的推論タスクの実行能力を調査する。我々は、モデルが全てのサブ問題に正しく答えられるが、全体的な解を生成できない頻度を測定し、この比率を構成性ギャップと呼ぶ。この比率は、事前学習で一緒に観測される可能性が低い複数の事実を組み合わせる必要がある答えを持つマルチホップ問題を出題することで評価します。GPT-3モデルでは、モデルサイズが大きくなるにつれて、シングルホップの質問応答性能はマルチホップの性能よりも速く向上し、したがって構成性のギャップは減少しないことが示されました。この驚くべき結果は、より強力なモデルがより多くの事実知識を記憶・想起する一方で、この種の構成的推論を行う能力には相応の向上が見られないことを示唆しています。
- そこで、我々は、暗黙的な推論ではなく、明示的な推論を行うことで、構成性のギャップを縮めることができることを実証するために、思考連鎖のような直観的な促しを行う方法を紹介する。さらに、[[chain of thought]]を改良した新しい方法である[[self-ask]]を紹介する。この方法では、最初の質問に答える前に、モデルが明示的に自分自身に質問し（そして答え）、フォローアップの質問をする。さらに、self-askの構造化されたプロンプトにより、フォローアップの質問に答えるために検索エンジンを簡単にプラグインできることを示し、これにより精度をさらに向上させる。

