---
title: "Dense Passage Retrieval for Open-Domain Question Answering"
---

> Open-domain question answering relies on efficient passage retrieval to select candidate contexts, where traditional sparse vector space models, such as TF-IDF or BM25, are the de facto method. In this work, we show that retrieval can be practically implemented using dense representations alone, where embeddings are learned from a small number of questions and passages by a simple [[dual-encoder framework]]. When evaluated on a wide range of open-domain QA datasets, our dense retriever outperforms a strong Lucene-BM25 system largely by 9%-19% absolute in terms of top-20 passage retrieval accuracy, and helps our end-to-end QA system establish new state-of-the-art on multiple open-domain QA benchmarks.
[https://arxiv.org/abs/2004.04906](https://arxiv.org/abs/2004.04906)
(DeepL)オープンドメインの質問応答は、候補文脈を選択するための効率的な文章検索に依存しており、[[TF-IDF]]や[[BM25]]のような従来の疎なベクトル空間モデルが事実上の手法である。この研究では、少数の質問と文章から単純なデュアルエンコーダーフレームワークによって埋め込みを学習することで、密な表現のみを用いて検索を実用的に実装できることを示す。幅広いオープンドメインのQAデータセットで評価したところ、我々の密な検索は、トップ20のパッセージの検索精度の点で、強力なLucene-BM25システムを9%～19%の絶対値で大きく上回り、我々のエンドツーエンドのQAシステムが複数のオープンドメインのQAベンチマークで新たな最先端を確立するのに役立つ。

[[DPR]]
[[Dense Passage Retrieval]]
[[Dense Passage Retriever]]


オープンドメイン QA における DPR の有効性検証 [PDF](https://www.anlp.jp/proceedings/annual_meeting/2021/pdf_dir/P7-15.pdf)
[【AI Shift Advent Calendar 2022】第13回対話システムシンポジウムで発表します | 株式会社AI Shift](https://www.ai-shift.co.jp/techblog/3019)

[[Two-Tower model]]
[https://www.youtube.com/watch?v=3giqIW2pIW4](https://www.youtube.com/watch?v=3giqIW2pIW4)
[【レポート】Google を支える推薦モデル「Two-Tower」とベクトル近傍検索技術 #GoogleCloudDay | DevelopersIO](https://dev.classmethod.jp/articles/google-cloud-day-2022-recommend-model-two-tower-session-report/)


