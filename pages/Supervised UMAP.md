---
title: "Supervised UMAP"
---

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- 1) ラベル活用（半教師あり）で“混在回避”を明示的に優先
    - Supervised UMAP（umap.UMAP(..., y=cluster_labels, target_weight=0.5–0.9)）
        - metric は埋め込みの性質に合わせて（L2正規化済なら cosine/angular が無難）。
        - n_neighbors=5–20（小さめで局所一貫性、分離が強まる）、min_dist=0.0–0.05（クラスターを締める）、repulsion_strength を上げる。
        - densMAP 版（densmap=True）は密度も保ちやすい（距離解釈が多少しやすくなる）。

[[UMAP]]
![image](https://gyazo.com/6d6c2cb2a60f302b3fe173177caba13a/thumb/1000)
