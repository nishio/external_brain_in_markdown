---
title: "ReAct(LLM)"
---

REACT: SYNERGIZING REASONING AND ACTING IN LANGUAGE MODELS
[https://arxiv.org/pdf/2210.03629.pdf](https://arxiv.org/pdf/2210.03629.pdf)
- While large language models (LLMs) have demonstrated impressive performance across tasks in language understanding and interactive decision making, their abilities for reasoning (e.g. chain-of-thought prompting) and acting (e.g. action plan generation) have primarily been studied as separate topics. In this paper, we explore the use of LLMs to generate both reasoning traces and task-specific actions in an interleaved manner, allowing for greater synergy between the two: reasoning traces help the model induce, track, and update action plans as well as handle exceptions, while actions allow it to interface with and gather additional information from external sources such as knowledge bases or environments. We apply our approach, named ReAct, to a diverse set of language and decision making tasks and demonstrate its effectiveness over state-of-the-art baselines in addition to improved human interpretability and trustworthiness. Concretely, on question answering (HotpotQA) and fact verification (Fever), ReAct overcomes prevalent issues of hallucination and error propagation in chain-of-thought reasoning by interacting with a simple Wikipedia API, and generating human-like task-solving trajectories that are more interpretable than baselines without reasoning traces.
- Furthermore, on two interactive decision making benchmarks (ALFWorld and WebShop), ReAct outperforms imitation and reinforcement learning methods by an absolute success rate of 34% and 10% respectively, while being prompted with only one or two in-context examples.
(DeepL)
- 大規模言語モデル（LLM）は、言語理解や対話的意思決定などのタスクにおいて素晴らしい性能を発揮しているが、推論（思考の連鎖を促すなど）と行動（行動計画の生成など）の能力は、主に別のテーマとして研究されてきた。この論文では、推論トレースとタスク固有のアクションの両方をインターリーブ方式で生成するLLMの使用を検討し、2つの間の相乗効果を高めることを可能にする。推論トレースは、モデルがアクションプランを誘導、追跡、更新し、例外を処理するのに役立ち、アクションによって知識ベースや環境などの外部ソースとインターフェースして追加情報を収集することができる。我々は、ReActと名付けられた我々のアプローチを、多様な言語タスクと意思決定タスクに適用し、人間の解釈可能性と信頼性の向上に加えて、最先端のベースラインに対する有効性を実証した。具体的には、質問応答（HotpotQA）と事実確認（Fever）において、ReActはシンプルなWikipedia APIと対話することにより、思考連鎖推論における幻覚やエラー伝播の問題を克服し、推論痕跡を持たないベースラインよりも解釈可能な人間らしいタスク解決軌跡を生成します。
- さらに、2つの対話型意思決定ベンチマーク（ALFWorldとWebShop）において、ReActは、1つか2つの文脈上の例で促されるだけで、模倣と強化学習法をそれぞれ34%と10%の絶対成功率で凌駕しています。

[[CoT]]([[Chain of Thought]])の改良
