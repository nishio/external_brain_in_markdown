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
