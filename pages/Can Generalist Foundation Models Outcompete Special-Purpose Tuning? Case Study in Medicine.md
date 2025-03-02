---
title: "Can Generalist Foundation Models Outcompete Special-Purpose Tuning? Case Study in Medicine"
---

from [[日記2023-12-04]]
Can Generalist Foundation Models Outcompete Special-Purpose Tuning? Case Study in Medicine
[https://arxiv.org/abs/2311.16452](https://arxiv.org/abs/2311.16452)
> [y_matsuwitter](https://twitter.com/y_matsuwitter/status/1731158086113751418) 小さなLLMを特化型で作ると良いみたいな言説はよく見るけど、推論能力などの影響か、GPT-4の方が特化型モデルより性能が高いとの研究。日本語とか医療とか特化させるから強いんです、というのは必ずしも正しくない。もちろん計算コストは落ちるし、運営元のルールやバイアスの影響を受けないので、その点では良いのかもしれないけど。
>
>  論文の要約
>  GPT-4などの汎用基盤モデルは、領域固有のトレーニングなしでも様々なタスクで驚くべき能力を示している。しかし、領域専門の能力を合わせ持つには、専門知識を用いたモデルのトレーニングが必要とする意見が一般的だ。 本研究では、医療関連のベンチマークを用いて、GPT-4に対するプロンプトエンジニアリングの探索的研究を行い、領域固有の微調整なしでも優れた専門性能力を発揮できることを示した。
>
>   [https://arxiv.org/abs/2311.16452](https://arxiv.org/abs/2311.16452)

> [icoxfog417](https://twitter.com/icoxfog417/status/1731305335456194591) GPT-4が特化型モデルの学習に使用されている医療系論文を学習していない保証はないので(Technical Reportに記載なし)、汎用的なモデル全体にこの結論が適用できるかはわからないと思う。
>  一般的にモデルが大きくなるほど学習データを増やす必要があるのでGPT-4が学習済みの可能性はゼロでないと思う

> [y_matsuwitter](https://twitter.com/y_matsuwitter/status/1731309738657526014) 論点が複数あって
>  ・GPT-4が特化型より強力であるか
>  ・汎用モデルが推論能力によって高い精度を達成し得るか
>  ・汎用モデルが推論能力と各ドメインの知識を学習に用いたことにより特化モデルより強化されるか
>  で、本論文は一つ目について書いていて、二つ目はおっしゃる通りで、3つ目があり得るのだとすると今後各大規模基盤モデルが各ドメインにおける高い能力を獲得することはあり得そうですね。

> [odashi_t](https://twitter.com/odashi_t/status/1731315250694369363) GPT-4で勝つためにエンジニアリングしまくった手法をMed PaLMに一切適用していないのでそもそもまともな比較になっていないですね。学習データのコンタミ以前の問題で、論文としてアレです。

