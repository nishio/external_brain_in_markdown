---
title: "Transformers meet Stochastic Block Models: Attention with Data-Adaptive Sparsity and Cost"
---

Transformers meet Stochastic Block Models: Attention with Data-Adaptive Sparsity and Cost
[https://papers.nips.cc/paper_files/paper/2022/file/9c93b3cd3bc60c0fe7b0c2d74a2da966-Paper-Conference.pdf#:~:text=URL%3A%20https%3A%2F%2Fpapers.nips.cc%2Fpaper_files%2Fpaper%2F2022%2Ffile%2F9c93b3cd3bc60c0fe7b0c2d74a2da966](https://papers.nips.cc/paper_files/paper/2022/file/9c93b3cd3bc60c0fe7b0c2d74a2da966-Paper-Conference.pdf#:~:text=URL%3A%20https%3A%2F%2Fpapers.nips.cc%2Fpaper_files%2Fpaper%2F2022%2Ffile%2F9c93b3cd3bc60c0fe7b0c2d74a2da966)

この論文は、注意メカニズムの計算コストを削減する新しいTransformerモデル「SBM-Transformer」を提案しています。主なポイントは以下の通りです:
- 各注意ヘッドは、入力データに基づいて適応的にスパース性を調整する確率的ブロックモデル(SBM)を持つ。これにより、データ依存の線形からフル注意までの間でコストを柔軟に選択できる。
- SBMからグラフをサンプリングし、その隣接行列を注意マスクとして使用。Straight-Through推定により、サンプリングを超えて勾配を伝播させ、予測損失に基づいてサンプリングされたエッジの確率を調整できる。
- 理論的に、SBM-Transformerは任意のシーケンス間関数のユニバーサルアプロキシメータであることを示した。
- LRAとGLUEベンチマークでの実験により、提案手法がフル注意のTransformerや既存の効率的な手法を上回ることを示した。
モデルはデータに適応してスパース性を調整できるため、入力に応じて計算コストを柔軟に変更できる点が新しい。理論的な表現力を維持しつつ、実用的なタスクでも優れた性能を示した。


[[注意機構の計算量削減]]
