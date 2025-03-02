---
title: "Step-by-Step(LLM)"
---

Show Your Work: Scratchpads for Intermediate Computation with Language Models
- Large pre-trained language models perform remarkably well on tasks that can be done “in one pass”, such as generating realistic text (Brown et al., 2020) or synthesizing computer programs (Chen et al., 2021; Austin et al., 2021). However, they struggle with tasks that require unbounded multi-step computation, such as adding integers (Brown et al., 2020) or executing programs (Austin et al., 2021).
- Surprisingly, we find that these same models are able to perform complex multistep computations—even in the few-shot regime—when asked to perform the operation “step by step”, showing the results of intermediate computations. In particular, we train Transformers to perform multi-step computations by asking them to emit intermediate computation steps into a “scratchpad”. On a series of increasingly complex tasks ranging from long addition to the execution of arbitrary programs, we show that scratchpads dramatically improve the ability of language models to perform multi-step computations.
[https://arxiv.org/abs/2112.00114](https://arxiv.org/abs/2112.00114)
(DeepL)自分の作品を見せる： 言語モデルによる中級計算のためのスクラッチパッド
- 事前に訓練された大規模な言語モデルは、現実的なテキストの生成（Brown et al., 2020）やコンピュータプログラムの合成（Chen et al., 2021; Austin et al., 2021）のような「1パスで」行えるタスクでは顕著に優れた性能を発揮します。しかし、整数の加算（Brown et al., 2020）やプログラムの実行（Austin et al., 2021）のような、束縛されない多段階の計算を必要とするタスクでは苦戦する。
- しかし意外なことに、同じモデルが、中間計算の結果を示しながら「ステップ・バイ・ステップ」で演算を行うよう求められた場合、数発体制であっても複雑な多段階計算を行うことができることがわかった。特に、Transformerに中間的な計算ステップを「スクラッチパッド」に出力させることで、多段階の計算を行うように訓練しています。長い足し算から任意のプログラムの実行まで、次第に複雑になっていく一連のタスクにおいて、スクラッチパッドが言語モデルの多段階計算の能力を劇的に向上させることを示す。


> [shodaiiiiii](https://twitter.com/shodaiiiiii/status/1637746876568174593/photo/1) 段階的に考えてみましょう(Let’s think step by step)より、正しい答えが得られるように、これを段階的に解決していきましょう(Let’s work this out in a step by step way to be sure we have the right answer)の方がPromptの命令文としてパフォーマンスが高いらしい
>  [https://arxiv.org/pdf/2211.01910.pdf…](https://arxiv.org/pdf/2211.01910.pdf…)
>  ![image](https://pbs.twimg.com/media/FrpxrA0aUAInCZv?format=png&name=small#.png)
この結果よりもこの論文が提案してる[[Automatic Prompt Engineer]]アルゴリズムが興味深い
- ![image](https://gyazo.com/c97ab673c62584d8f95261439818f1b4/thumb/1000)
