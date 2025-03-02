---
title: "Multimodal Transformer with a Low-Computational-Cost Guarantee"
---

[https://ar5iv.labs.arxiv.org/html/2402.15096v1](https://ar5iv.labs.arxiv.org/html/2402.15096v1)
この論文では、マルチモーダルTransformerの計算コストを削減するための新しい注意機構であるLow-Cost Multimodal Transformer (LoCoMT)を提案しています。
主なポイントは以下の通りです。
- LoCoMTは、各注意ヘッドに異なるマルチモーダル注意パターンを割り当てることで、マルチモーダル信号を柔軟に制御しつつ、既存のマルチモーダルTransformerと比較して理論的に計算コストを削減できることを保証。
- AudiosetとMedVidCLの2つのマルチモーダルデータセットでの実験により、LoCoMTはGFLOPsを削減するだけでなく、確立されたモデルと同等以上の性能を発揮することを実証。
- 様々なLoCoMTの設定における性能と効率のトレードオフを調査し、パフォーマンスをほとんど落とさずにGFLOPsを半分近く節約できることを示した。
- 層ごとに異なる注意パターンを割り当てる影響を探り、低レベル層ではself-attentionがパフォーマンス向上に役立ち、高レベル層ではランダムな注意パターンでも十分に機能することを発見。

以上のように、LoCoMTは計算コストを大幅に削減しつつ高い性能を維持できる、効率的なマルチモーダル融合のための有望なアプローチであると結論づけています。

[[注意機構の計算量削減]]
