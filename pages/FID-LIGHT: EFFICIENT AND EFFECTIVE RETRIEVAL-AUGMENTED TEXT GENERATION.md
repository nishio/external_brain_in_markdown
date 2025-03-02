---
title: "FID-LIGHT: EFFICIENT AND EFFECTIVE RETRIEVAL-AUGMENTED TEXT GENERATION"
---

> [[Retrieval-augmented generation]] models offer many benefits over standalone language models: besides a textual answer to a given query they provide provenance items retrieved from an updateable knowledge base. However, they are also more complex systems and need to handle long inputs. In this work, we introduce FiDLight to strongly increase the efficiency of the state-of-the-art retrieval-augmented FiD model, while maintaining the same level of effectiveness. Our FiD-Light model constrains the information flow from the encoder (which encodes passages separately) to the decoder (using concatenated encoded representations). Furthermore, we adapt FiD-Light with re-ranking capabilities through textual source pointers, to improve the top-ranked provenance precision. Our experiments ona diverse set of seven knowledge intensive tasks (KILT) show FiD-Light consistently improves the Pareto frontier between query latency and effectiveness.
>  FiD-Light with source pointing sets substantial new state-of-the-art results on six KILT tasks for combined text generation and provenance retrieval evaluation, while maintaining reasonable efficiency
(DeepL)[[検索補強型生成モデル]]は、単体の言語モデルと比較して多くの利点を提供する。与えられたクエリに対するテキストの答えの他に、更新可能な知識ベースから取得した実績項目を提供する。しかし、より複雑なシステムであり、長い入力を扱う必要がある。本研究では、FiDLightを導入することで、最新の検索補強型FiDモデルの効率を、同レベルの有効性を維持しながら大幅に向上させる。我々のFiD-Lightモデルは、エンコーダ（パッセージを別々にエンコードする）からデコーダ（エンコードされた表現を連結して使用する）までの情報の流れを制約する。さらに、我々はFiD-Lightにテキストソースポインタによる再ランキング機能を適応させ、トップランクの実績精度を向上させた。7つの知識集約型タスク（KILT）の多様なセットを用いた実験により、FiD-Lightはクエリの待ち時間と有効性の間のパレートフロンティアを一貫して改善することが示された。
ソースポインティングを用いたFiD-Lightは、テキスト生成と実績検索を組み合わせた評価のための6つのKILTタスクにおいて、合理的な効率を維持しながら、実質的に新しい最先端の結果を示した。

[2209.14290 FiD-Light: Efficient and Effective Retrieval-Augmented Text Generation](https://arxiv.org/abs/2209.14290)


[[FID]]
- [[Fusion in Decoder]]
[[RETRIEVAL-AUGMENTED TEXT GENERATION]]
