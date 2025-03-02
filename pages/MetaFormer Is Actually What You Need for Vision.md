---
title: "MetaFormer Is Actually What You Need for Vision"
---

[https://arxiv.org/abs/2111.11418](https://arxiv.org/abs/2111.11418)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>この論文では、[[Transformer]]のアーキテクチャから[[注意機構]]（トークンミキサー）を抽象化した一般的なアーキテクチャ「[[MetaFormer]]」を提案しています。主な内容は以下の通りです。
- Transformerや最近のMLPモデルの成功は、主にMetaFormerアーキテクチャに起因すると主張。トークンミキサーの種類は重要ではない。
- これを検証するため、トークンミキサーに極めてシンプルなプーリング演算を用いたモデル「[[PoolFormer]]」を提案。ImageNetで最新のTransformer/MLPモデルと同等以上の性能を達成。
- PoolFormerを物体検出、インスタンスセグメンテーション、意味セグメンテーションに適用し、ResNetなどの従来手法を上回る性能を確認。
- 今後はMetaFormerアーキテクチャそのものの改良に注力すべきだと提言。PoolFormerは、MetaFormer設計のベースラインとして活用できる。
つまり本論文は、Transformerの成功要因は注意機構ではなく、MetaFormerと呼ぶ残りのアーキテクチャにあると指摘し、具体的な検証実験を行って、MetaFormerの重要性を示唆した意欲的な内容と言えます。

[[PoolFormer]]は、Transformerの注意機構（attention）をプーリング（pooling）に置き換えたシンプルなモデルアーキテクチャです。主なポイントは以下の通りです。
1. Transformerを一般化したMetaFormerというアーキテクチャを提案。MetaFormerではトークン混合（token mixer）の方法を特定していない。
2. MetaFormerでトークン混合にプーリングを使ったモデルがPoolFormer。パラメータを学習するattentionやSpatial MLPに比べ、プーリングは極めてシンプル。
3. PoolFormerは、ImageNet分類などのタスクでTransformerやMLP系モデルと同等以上の性能を達成。パラメータ数や計算量ははるかに少ない。
4. これは、モデルの性能にとってトークン混合の方法よりもMetaFormerの全体アーキテクチャの方が重要という著者の主張を裏付ける。
5. PoolFormerの性能は、Transformerの成功が主にattentionによるのではなく、MetaFormerの全体構造に由来することを示唆している。

つまり本論文は、Transformerを抽象化したMetaFormerこそが、様々なタスクで高い性能を発揮するために本質的に重要だと主張しています。

[[注意機構の計算量削減]]
