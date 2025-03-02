
Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
- We explore how generating a chain of thought—a series of intermediate reasoning steps—significantly improves the ability of large language models to perform complex reasoning. In particular, we show how such reasoning abilities emerge naturally in sufficiently large language models via a simple method called chain-ofthought prompting, where a few chain of thought demonstrations are provided as exemplars in prompting.
- Experiments on three large language models show that chain-of-thought prompting improves performance on a range of arithmetic, commonsense, and symbolic reasoning tasks. The empirical gains can be striking. For instance, prompting a PaLM 540B with just eight chain-of-thought exemplars achieves state-of-the-art accuracy on the GSM8K benchmark of math word problems, surpassing even finetuned GPT-3 with a verifier.
- [https://arxiv.org/pdf/2201.11903.pdf](https://arxiv.org/pdf/2201.11903.pdf)
(DeepL)大規模言語モデルにおける推論を引き出す思考連鎖型プロンプティング
- 我々は、思考の連鎖（一連の中間推論ステップ）を生成することで、大規模言語モデルが複雑な推論を行う能力をいかに大幅に向上させるかを探求する。特に、思考連鎖プロンプトと呼ばれる、いくつかの思考連鎖のデモンストレーションをプロンプトの模範として提供する簡単な方法によって、十分に大きな言語モデルにおいて、そのような推論能力が自然に現れることを示す。
- 3つの大規模言語モデルを用いた実験により、思考連鎖プロンプトが算術、常識、記号の推論タスクのパフォーマンスを向上させることが示された。経験的な向上は顕著である。例えば、PaLM 540Bにわずか8個の思考連鎖の模範解答を与えることで、数学の単語問題のGSM8Kベンチマークで最先端の精度を達成し、検証機を用いて細かく調整したGPT-3をも凌ぐ。

![image](https://gyazo.com/f21f8aafa600f51e984c7de12c2a3d7e/thumb/1000)
[[LangChain Glossary]]

推論タスクが苦手なのでPromptingで改善する
- 事例で思考の過程を入れる

Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
[https://arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903)

[[Zero-Shot CoT]]
