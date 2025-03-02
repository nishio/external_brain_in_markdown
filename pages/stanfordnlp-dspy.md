---
title: "stanfordnlp/dspy"
---

[[自動プロンプトエンジニアリング]]
[https://github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>[[DSPy]]は、言語モデル(LM)のプロンプトや重みを最適化するためのフレームワークであり、特にLMがパイプライン内で1回以上使用される場合に有効です。DSPyは、プログラムの流れ(モジュール)と各ステップのパラメータ(LMプロンプトと重み)を分離し、LMを駆動するアルゴリズムを提供して、指定されたメトリックを最大化するようにプロンプトや重みを調整することができます。

DSPyを使用することで、GPT-3.5やGPT-4などの強力なモデルを、タスクに対してより信頼性の高いものに仕立て上げることができます。DSPyのオプティマイザは、同じプログラムを各LMに適した命令やfew-shotプロンプト、重み更新にコンパイルします。これにより、LMとそのプロンプトがデータから学習可能なシステムの最適化可能な部品として扱えるようになります。

つまり、DSPyを使うことで、プロンプトのハッキングや手作業でのデータ生成の代わりに、体系的なアプローチで難しいタスクに取り組むことができるようになるのです。

DSPyに関連する主要な論文が複数あります。
- "[[DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines]]" (2023年10月)
    - この論文では、DSPyフレームワークの概要と、その背後にある主要なアイデアについて説明しています。宣言的な言語モデルの呼び出しを自己改善するパイプラインにコンパイルするという概念を紹介し、DSPyの設計と実装について詳しく述べています。
- "[[DSPy Assertions: Computational Constraints for Self-Refining Language Model Pipelines]]" (2023年12月)
    - この論文では、DSPyアサーションという概念を導入しています。これは、言語モデルのパイプラインの振る舞いに制約を課すことで、自己改善プロセスをガイドするものです。アサーションの定式化と、それがDSPyプログラムの品質向上にどのように役立つかを示しています。
- "[[Demonstrate-Search-Predict: Composing Retrieval and Language Models for Knowledge-Intensive NLP]]" (2022年12月)
    - この論文は、DSPyの前身となるDemonstrate-Search-Predict (DSP)フレームワークを紹介しています。知識集約型のNLPタスクに対して、検索モデルと言語モデルを組み合わせる方法を提案し、その有効性を実証しています。DSPyは、このアイデアをさらに発展させたものと言えます。

これらの論文は、DSPyの進化の過程を示すとともに、フレームワークの主要なアイデアと技術的な詳細を提供しています。DSPyを深く理解するためには、これらの論文を参照することが有益でしょう。


> [hrjn](https://twitter.com/hrjn/status/1786994101646414236) 西尾さんの投稿で気になっていた dspy。まだ触ってないのでよくわからんけど、つまりプロンプトの最適化のベストプラクティスを勝手にやってくれるフレームワークなのかな。
>  langchainがIFTTTならDSpyはpytorch?scrapbox.io

> [nishio](https://twitter.com/nishio/status/1787021308116787515) もう少し詳しいやつを書いた。目的関数が軽量に定義できるなら(そしてQAの正解率はそう)プロンプトを変更してスコアを計算することの繰り返しで、プロンプトを自動的にチューニングできる、というのは大まかな技術進化の方向性としてはそうだと思う
> [[DSPy]]

> [nishio](https://twitter.com/nishio/status/1787021799521472553) プロンプトをハイパーパラメータの空間とみなすと、離散的で超高次元だから効率良いチューニングが難しそー、というところと、目的関数を軽量に実装できないときはどうするの？LLMを叩きまくるの？というところが問題

