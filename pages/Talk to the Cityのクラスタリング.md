---
title: "Talk to the Cityのクラスタリング"
---

2024-05-26
[[Talk to the City]]の[[クラスタリング]]
[source](https://github.com/AIObjectives/talk-to-the-city-reports/blob/main/scatter/pipeline/steps/clustering.py)

[[BERTopic]]
- これが内部的にHDBSCANとUMAPを使うようだ
    - [[HDBSCAN]]
        - [HDBSCAN — scikit-learn 1.5.0 documentation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.HDBSCAN.html)
        - > HDBSCAN - Hierarchical Density-Based Spatial Clustering of Applications with Noise. Performs [[DBSCAN]] over varying epsilon values and integrates the result to find a clustering that gives the best stability over epsilon. This allows HDBSCAN to find clusters of varying densities (unlike DBSCAN), and be more robust to parameter selection.
    - [[UMAP]]

2025-06-06
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>に解説させる
- 処理フロー
    - UMAP で高次元埋め込みを 2 次元に射影
    - HDBSCAN ＋ BERTopic で 「トピックの確率」 を推定
    - 射影後の 2D 座標を使って Spectral Clustering で 「最終クラスタ」 を決定
    - 結果を clusters.csv に保存（各 argument を x–y 位置・確率・cluster-id 付きで出力）


[[UMAP]]後の座標データの[[Spectral Clustering]]と、文書とUMAP後の座標データを内部で[[HDBSCAN]]する[[BERTopic]]に与えたものの結果とを、前者のクラスタIDと後者のprobabilityで束ねて出力している。それクラスタが対応づかない可能性あるのでは？
:

```
cluster_labels = spectral_model.fit_predict(umap_embeds)
result = topic_model.get_document_info(
    docs=docs,
    metadata={
        **metadatas,
        "x": umap_embeds[:, 0],
        "y": umap_embeds[:, 1],
    },
)
```


:

```
result = result[['arg-id', 'x', 'y', 'probability']]
result['cluster-id'] = cluster_labels
```
