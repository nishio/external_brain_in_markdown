---
title: "Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering"
---

> Generative models for open domain question answering have proven to be competitive, without resorting to external knowledge. While promising, this approach requires to use models with billions of parameters, which are expensive to train and query. In this paper, we investigate how much these models can benefit from retrieving text passages, potentially containing evidence. We obtain state-of-the-art results on the Natural Questions and TriviaQA open benchmarks. Interestingly, we observe that the performance of this method significantly improves when increasing the number of retrieved passages. This is evidence that generative models are good at aggregating and combining evidence from multiple passages.
[https://arxiv.org/abs/2007.01282](https://arxiv.org/abs/2007.01282) (2020)
(DeepL)オープンドメインの質問応答のための生成モデルは、外部の知識に頼ることなく、競争力があることが証明されている。このアプローチは有望ではあるが、数十億のパラメータを持つモデルを使用する必要があり、学習や問い合わせにコストがかかる。本論文では、これらのモデルが、潜在的に証拠を含むテキストを検索することによって、どれだけ恩恵を受けることができるかを調査する。我々はNatural QuestionsとTriviaQAのオープンベンチマークで最先端の結果を得た。興味深いことに、検索される文章数を増やすと、この手法の性能が大幅に向上することが確認された。これは、生成モデルが複数の文章からの証拠を集約し、組み合わせることに長けている証拠である。
[[Fusion-in-Decoder]]
