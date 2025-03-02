---
title: "Chain of Thought"
---

# 2023年に人間が書いたもの
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

# 2025年に書いたもの(+AIによる解説)
[[Chain-of-Thought Prompting Elicits Reasoning in Large Language Models]]
[https://arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903)
2025-02-01 [[CoT]]を知らない人がいてびっくりしたんだけど、冷静に考えると2022年の論文なので知らない方が普通である
- 3年経って、「使って当然」のレベルの技術になり、これを使うことを前提としてモデルが訓練されるようになった
- [[GPT o1]]や[[DeepSeek]]によってこれによる思考過程がエンドユーザーにも見えるようになった

## [[o3-mini-high]]
この文書は、大規模言語モデルにおける「Chain-of-Thought（CoT）Prompting」の手法とその効果について詳細に検証した研究内容をまとめたものです。

【要点】
- Chain-of-Thought Promptingとは
    - 問題に対して最終回答だけでなく、中間推論過程（思考の連鎖）を生成させることで、複雑な多段階の推論を実現する手法です。

- 実験結果
    - 数学問題（GSM8K、SVAMP、ASDiv、AQuA、MAWPS）や常識・象徴的推論タスク（CSQA、StrategyQA、Date Understanding、Sports Understanding、SayCan）において、CoT Promptingを利用した場合、従来のfew-shot promptingよりも大幅な性能向上が確認されました。
    - 特にモデルサイズが大きくなる（例：PaLM 540B、GPT-3 175B）と、CoTによる効果が顕著になりました。

- ロバスト性とエラー解析
    - 複数のプロンプト例や異なるアノテーターによる記述でも効果が確認され、計算ミスや記号の扱いの誤りなどを外部計算機で補正する手法も検討されました。

【結論】
Chain-of-Thought Promptingは、従来の単一回答型のプロンプトに比べ、複雑な多段階推論が要求されるタスクで大きな性能向上を示しており、今後の大規模言語モデル活用やタスク適用において非常に有望なアプローチと考えられます。

## o1 Pro
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
要約（簡潔版）
「Chain-of-Thought Prompting（思考過程プロンプト）」は、大規模言語モデルに対して解答の中間推論過程（チェーン・オブ・ソート）を少数例のサンプルとともに与えることで、複雑な推論問題（算数文章題、常識推論、記号操作など）の性能を大きく向上させる手法である。特に数百億～数千億パラメータ規模のモデルになると、従来の“答えだけを示す”プロンプトよりも大幅な精度向上が得られ、たとえば数学問題集（GSM8K）では最先端を上回る結果を達成した。興味深い点として、チェーン・オブ・ソートの有効性は「ある規模以上」から顕在化する（小規模モデルでは効果が小さい）。また、チェーン・オブ・ソートによって中間推論の可視化も可能になるが、必ずしも正しい推論ばかりとは限らない点は今後の課題である。

解説（ポイント説明）
- 背景と着想
    - 従来の大規模言語モデルは「入力→出力」を直接マッピングするプロンプトでは複雑な推論に弱いことが多かった。
    - 「途中の思考過程（推論のステップ）を自然言語で書き下す」例を数件提示し、モデル自身にも解答前にステップを出力させると、推論精度が大きく向上する。

- 方法：Chain-of-Thought Prompting
    - 数件の例題を「問題→（思考過程の文章）→最終答え」という形で提示する。
    - モデルは学習や追加のパラメータ更新なしに、提示例を手がかりに中間推論文を生成しつつ結論に至る。

- 実験結果の特徴
    - 算数文章題（GSM8Kなど）で顕著な性能向上：例として、PaLM 540Bモデルはチェーン・オブ・ソートによって既存手法を超えるSOTAを達成。
    - 常識推論や記号的操作でも効果があり、Chain-of-Thought Promptingにより回答精度が大きく高まった。
    - 小型モデルではほとんど改善が見られず、**「大規模モデルでこそ効果が顕著」**という“出現的能力”が確認された。

- 追加分析
    - 単に中間に「式だけ」書かせるなどの変形ではほとんど効果が得られず、「自然言語でステップを追う」ことが鍵となる。
    - チェーン・オブ・ソートの書き方やサンプル例の選び方に多少の影響はあるが、大筋でどの注釈スタイルでも標準プロンプトを上回る。
    - 解答が当たっていても推論過程の一部が誤っていたり、逆に途中までは正しくても結果が間違うケースもある（推論内容に絶対の信頼は置けない）。

- 意義と課題
    - 意義: 従来の「答えのみ」の出力と比較し、大規模モデルが複雑な思考ステップを扱える可能性を引き出す簡便な手法として注目される。
    - 課題: 論理的整合性が常に保証されるわけではなく、計算コストやサイズ依存など実用面のハードルも残る。

本研究は「適切な例題とともに思考過程を明示する」だけで、大規模言語モデルの多段推論能力を大きく伸ばせることを示した点にある。すなわち、大きなパラメータ数を活かしたモデルであれば、チェーン・オブ・ソートの形で少数例を示すだけで、多段推論が可能になるという発見がポイントである。

