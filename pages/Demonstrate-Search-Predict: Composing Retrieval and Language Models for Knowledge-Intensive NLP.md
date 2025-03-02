---
title: "Demonstrate-Search-Predict: Composing Retrieval and Language Models for Knowledge-Intensive NLP"
---


[2212.14024 Demonstrate-Search-Predict: Composing retrieval and language models for knowledge-intensive NLP](https://arxiv.org/abs/2212.14024)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文は、言語モデル(LM)と検索モデル(RM)を組み合わせた新しいフレームワークDEMONSTRATE–SEARCH–PREDICT (DSP)を提案している。主なポイントは以下の通りです。
1. DSPでは、LMとRMの間で自然言語テキストをやり取りすることで、複雑な知識集約型タスクを解くパイプラインを構築できる。
2. DSPプログラムは、デモの自動生成(DEMONSTRATE)、関連情報の検索(SEARCH)、根拠のある予測(PREDICT)の3つのステージで構成される。
3. DEMONSTRATEでは少数の訓練例からパイプラインの中間表現に自動でアノテーションを付与。SEARCHでは対話の文脈を考慮した質問の書き換えやマルチホップ検索を実現。PREDICTでは複数の検索結果を統合して最終出力を生成。
4. DSPプログラムをオープンドメイン質問応答、マルチホップ質問応答、対話質問応答の3タスクに適用し、既存手法から37-120%の精度向上を達成。
5. DSPにより、事前学習済みのLMとRMをモジュールとして組み合わせ、新しいドメインに素早く適応できるAIシステムを開発できる可能性が示された。
DSPは、LMとRMをうまく連携させることで、より洗練されたインコンテキスト学習システムを実現するための基盤を提供するフレームワークだと言える。