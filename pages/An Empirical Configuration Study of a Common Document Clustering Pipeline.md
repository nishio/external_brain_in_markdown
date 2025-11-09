---
title: "An Empirical Configuration Study of a Common Document Clustering Pipeline"
---

[An Empirical Configuration Study of a Common Document Clustering Pipeline(PDF)](https://aclanthology.org/2023.nejlt-1.7.pdf)
[[Anton Eklund+ 2023]]
![image](https://gyazo.com/071aa00fa9cb953e7a0d3a988816cfc6/thumb/1000)

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>[[文書クラスタリング]]の体系的比較（NEJLT 2023）
- BERT 埋め込み＋次元削減（UMAP/PCA）＋クラスタリング（k‑means/HDBSCAN）のパイプラインを複数データセット（SNACK/AG News/Reuters）で比較。
- 結果として 「bert_umap_hdbscan」または「bert_umap_kmeans」が最良であることが多い。次元数は 10–15 次元で性能が頭打ちになりやすく、2D など極端な低次元は不利。時間面では UMAP の計算コストは n_neighbors に強く依存（20→数秒、1280→数百秒）という計測も示されています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- [[埋め込みベクトルをUMAPしてからクラスタリング]]することに関して、「UMAPしてからクラスタリングするのはあり？」という問いは適切ではなくUMAPで何次元にするのかが重要という研究結果
    - 2次元に落とすのは明らかに悪い
    - 5~10次元ならだいぶマシになる
    - 15次元以上にしてもそれ以上良くはならなさそう
