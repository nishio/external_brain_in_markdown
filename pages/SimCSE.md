
[SimCSEとベクトル検索で類似内容を掲出し、利便性を改善する（Yahoo!検索の関連検索ワードでの事例） - Yahoo! JAPAN Tech Blog](https://techblog.yahoo.co.jp/entry/2023050830422060/)
- [[ベクトル検索]]
- > 自然言語処理のさまざまなタスクにおいて、BERTの有効性が示され、広く利用されるようになってきました。しかし、今回のベクトル検索のように文ベクトルを利用したタスクには不適切だと考えられます。理由は、BERTには異方性という特徴があると確認されているためです［2］。これは、文ベクトルが特定の方向に偏っているために単語の類似性を適切に捉えきれないというものです。
- >  SimCSEは、正例のベクトル同士は距離が近くなるようにし、かつベクトルの分布が一様になるように修正することで異方性を解消しました。
    - [[BERTの異方性]]

[(2104.08821) SimCSE: Simple Contrastive Learning of Sentence Embeddings](https://arxiv.org/abs/2104.08821)

[princeton-nlp/SimCSE: EMNLP'2021: SimCSE: Simple Contrastive Learning of Sentence Embeddings](https://github.com/princeton-nlp/SimCSE)


[https://www.slideshare.net/DeepLearningJP2016/dlsimcse-simple-contrastive-learning-of-sentence-embeddings-emnlp-2021](https://www.slideshare.net/DeepLearningJP2016/dlsimcse-simple-contrastive-learning-of-sentence-embeddings-emnlp-2021)

BERTとの比較
- 異方性

埋め込み
[[Embedding]]
