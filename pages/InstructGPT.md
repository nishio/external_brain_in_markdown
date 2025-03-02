---
title: "InstructGPT"
---

[[Training language models to follow instructions with human feedback]] (4 Mar 2022)
> Making language models bigger does not inherently make them better at following a user's intent. For example, large language models can generate outputs that are untruthful, toxic, or simply not helpful to the user. In other words, these models are not aligned with their users. In this paper, we show an avenue for aligning language models with user intent on a wide range of tasks by fine-tuning with human feedback. Starting with a set of labeler-written prompts and prompts submitted through the OpenAI API, we collect a dataset of labeler demonstrations of the desired model behavior, which we use to fine-tune GPT-3 using supervised learning. We then collect a dataset of rankings of model outputs, which we use to further fine-tune this supervised model using [[reinforcement learning from human feedback]]. We call the resulting models InstructGPT. In human evaluations on our prompt distribution, outputs from the 1.3B parameter InstructGPT model are preferred to outputs from the 175B GPT-3, despite having 100x fewer parameters. Moreover, InstructGPT models show improvements in truthfulness and reductions in toxic output generation while having minimal performance regressions on public NLP datasets. Even though InstructGPT still makes simple mistakes, our results show that fine-tuning with human feedback is a promising direction for aligning language models with human intent.
- (DeepL)言語モデルを大きくしても、ユーザーの意図に沿うことができるようになるとは限りません。例えば、大きな言語モデルは、真実味のない、有害な、あるいは単にユーザーにとって役に立たない出力を生成することがあります。言い換えれば、これらのモデルはユーザーと一致alignしていない。
    - These models are not aligned with their users
- 本論文では、人間のフィードバックによって微調整することで、幅広いタスクにおいて言語モデルをユーザーの意図に沿うようにする道を示す。まず、ラベラーが書いたプロンプトとOpenAI APIを通じて提出されたプロンプトのセットから始め、我々はラベラーが望ましいモデルの動作を示すデータセットを収集し、これを用いて教師あり学習でGPT-3を微調整する。さらに、モデルの出力に対するランキングのデータセットを収集し、人間のフィードバックからの強化学習(reinforcement learning from human feedback, [[RLHF]])を用いて、この教師ありモデルをさらに微調整する。このようにして得られたモデルを[[InstructGPT]]と呼ぶ。
- 我々のプロンプト分布に対する人間の評価では、パラメータが100倍少ないにもかかわらず、13億パラメータのInstructGPTモデルの出力は、175BのGPT-3の出力よりも好まれました。さらに、InstructGPTモデルは、真実性の向上と有害な出力生成の削減を示し、公開NLPデータセットでの性能後退は最小限である。InstructGPTはまだ単純なミスを犯すものの、この結果は、人間のフィードバックによる微調整が、言語モデルを人間の意図に合わせるための有望な方向性であることを示しています。

[InstructGPTの実装解説 - Qiita](https://qiita.com/thmd9726/items/c9fbf0886fb9ab5672e2)

