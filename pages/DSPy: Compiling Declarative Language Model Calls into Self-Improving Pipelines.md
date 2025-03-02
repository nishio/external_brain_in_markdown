---
title: "DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines"
---

[2310.03714 DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines](https://arxiv.org/abs/2310.03714)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文は、言語モデル(LM)を用いたパイプライン構築のためのプログラミングモデルDSPyを提案している。主なポイントは以下の通りです。
- DSPyでは、LMの呼び出しを[[宣言的モジュール]]に抽象化し、それらを組み合わせて[[テキスト変換グラフ]]を構築する。
- DSPyモジュールはパラメータ化されており、プロンプティングやファインチューニング、データ拡張、推論などの技術を学習・組み合わせることができる。
- DSPyコンパイラは、任意のDSPyプログラムを最適化し、指定されたメトリクスを最大化する。
- 数学の文章問題や複数ステップの質問応答などのケーススタディで、数行のDSPyプログラムがGPT-3.5やLlama2-13bを自己改善し、手作りのプロンプトを上回る性能を短時間で達成した。
- 770MパラメータのT5など、オープンで比較的小さなLMでも、DSPyにより高性能なパイプラインを構築できた。
DSPyは、LMパイプラインをモジュール化し、プロンプトの最適化を自動化することで、LMを用いたシステム構築を効率化・高度化するための基盤を提供している。
