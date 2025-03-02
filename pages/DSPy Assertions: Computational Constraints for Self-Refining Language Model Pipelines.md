---
title: "DSPy Assertions: Computational Constraints for Self-Refining Language Model Pipelines"
---

[2312.13382 DSPy Assertions: Computational Constraints for Self-Refining Language Model Pipelines](https://arxiv.org/abs/2312.13382)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文では、言語モデル(LM)パイプラインに対する計算制約を表現するための新しいプログラミング構造体であるLM Assertionsを提案している。主なポイントは以下の通りです。
1. LM Assertionsは、LMの出力が満たすべき条件をブール式で表現する。AssertとSuggestの2種類がある。Assertは重大な制約違反でパイプラインを停止し、Suggestは軽微な制約違反を示唆する。
2. DSPyプログラミングモデルにLM Assertionsを統合し、制約違反時のバックトラック・再試行のセマンティクスを定義した。制約違反時は、LMに過去の出力とエラーメッセージを与えて再生成させる。
3. LM Assertionsを使って、制約を満たす例を自動生成し、LMパイプラインの最適化に利用できる。また、制約違反の反例とその修正も自動生成できる。
4. 4つのタスクで評価したところ、LM Assertionsによりパイプラインが制約を満たす割合が大幅に向上し(最大164%)、高品質な出力の割合も向上した(最大37%)。
5. 制約間の競合などの課題もあるが、LM Assertionsにより、開発者が望む計算制約をLMパイプラインに指定し、自動的に満たすことが可能になる。
LM Assertionsは、信頼性の高いLMパイプラインをより高度に構築するための基盤を提供するものといえる。
