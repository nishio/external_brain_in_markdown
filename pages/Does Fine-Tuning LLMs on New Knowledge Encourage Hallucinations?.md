---
title: "Does Fine-Tuning LLMs on New Knowledge Encourage Hallucinations?"
---

> [hillbig](https://x.com/hillbig/status/1792334744522485954) LLMに新しい知識をファインチューニングを用いて導入しようとすると、事前学習時に得た知識もハルシネーションするようになり性能が悪化する。事前学習時に知らない知識を獲得するのに時間がかかり複数回参照すると過学習するため。事前学習時に学んだが、使えていない知識をファインチューニングで引き出すのには有効。
>  そのため、ファインチューニング時に、モデルが知らないデータをフィルタリングするのは有効であるし、「これは知らない情報」とラベルを付けておくのも有効。
>  今のAIモデルは結局習が遅いという問題と、既存の知識/記憶に影響を与えず新しい知識/記憶を獲得できないという問題を解決できていない。人は学習が速く、新しい学習結果が既存に干渉しないようにできるので方法はあるはず。記憶の定着（consolidation）のような仕組みがまだないように思える。
>  [https://arxiv.org/abs/2405.05904](https://arxiv.org/abs/2405.05904)
