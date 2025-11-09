---
title: "Considerably Improving Clustering Algorithms Using UMAP Dimensionality Reduction Technique: A Comparative Study"
---

「UMAPで次元削減してからクラスタリングすると、精度と計算時間が大きく改善する」という研究

Considerably Improving Clustering Algorithms Using UMAP Dimensionality Reduction Technique: A Comparative Study
[[Allaoui et al. 2020]]
[PDF](https://link.springer.com/content/pdf/10.1007/978-3-030-51935-3_34.pdf)
![image](https://gyazo.com/47a4ecc636b7a8303f7a26e9178fcb4e/thumb/1000)


<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
要点（結論）
- 高次元データをUMAPで低次元に埋め込んでから K-means／GMM／凝集型階層／HDBSCAN をかけると、精度（Accuracy/NMI）も実行時間も改善。特にGMMや階層系が大きく伸びるケースが多い。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
- 対象は画像系の5データセット（MNIST、Fashion-MNIST、UMIST Faces、PenDigits、USPS）。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))

実験の中身
- 比較アルゴリズム：K-means／GMM／Agglomerative／HDBSCAN を、元の特徴量空間 vs UMAP後の埋め込み空間で実行して比較。評価は Accuracy と NMI。([ACM Digital Library](https://dl.acm.org/doi/10.1007/978-3-030-51935-3_34?utm_source=chatgpt.com))
- 結果例（論文の表より）：
    - K-means（MNIST）：Accuracy 0.53 → 0.91、NMI 0.48 → 0.85。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
    - K-means（UMIST Faces）：0.43 → 0.74。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
    - Agglomerative（USPS）：0.68 → 0.96。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
    - GMM は5データ中3つで Accuracy 34%超、NMI 25%超の改善と記述。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
- 計算時間：HDBSCANは（元空間だと）26分超 → UMAP後は約5秒（MNIST/F-MNIST）まで短縮。([PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC7340901/?utm_source=chatgpt.com))

どう解釈すべきか（実務示唆）
- 「UMAP→クラスタリング」は有力な前処理：クラスタが絡み合ったり不要次元が多いときに、分離性と計算効率を上げやすい。後続の研究やサーベイもこの方針を支持。([SpringerLink](https://link.springer.com/article/10.1007/s10618-023-00980-2?utm_source=chatgpt.com))
- ただし2次元可視化用の埋め込みにそのままクラスタリングするのは慎重に。UMAP作者側ドキュメントも「議論はある」と注意喚起。クラスタ目的なら 2Dに限らず10～50次元程度で埋め、そこでHDBSCAN等を回すのが推奨。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/clustering.html?utm_source=chatgpt.com))
- ハイパラの目安：
    - `n_neighbors` は局所/大域のトレードオフ（小さくすると局所、クラスタ寄り）。
    - `min_dist` はクラスタを締めるなら小さめ（0～0.3目安）。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/parameters.html?utm_source=chatgpt.com))
- テキストなど他領域：文書クラスタリングの実験では、UMAPで15次元以上に落としてからクラスタリングすると安定、チューニングの影響は限定的という報告も。([ACLアントロジー](https://aclanthology.org/2023.nejlt-1.7.pdf?utm_source=chatgpt.com))

限界・注意
- 対象は画像系5データセット中心で、他ドメインへの一般化は要検証。([ResearchGate](https://www.researchgate.net/publication/340388772_Considerably_Improving_Clustering_Algorithms_Using_UMAP_Dimensionality_Reduction_Technique_A_Comparative_Study?utm_source=chatgpt.com))
- 次元削減は近傍関係を歪める可能性があるため、トラストワースネス等で埋め込み品質を点検しつつ、元空間でのクラスタ結果とも比較するのが安心。([umap-learn.readthedocs.io](https://umap-learn.readthedocs.io/en/latest/clustering.html?utm_source=chatgpt.com))
必要なら、この論文の数値をもう少し整理して「どのアルゴリズム×データで何が効いたか」を表にして出します。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- この研究は[[BERTopic: Neural topic modeling with a class-based TF-IDF]]がUMAPすることの正当化のために言及している
- が、データセットは全部画像系であり、各軸の間に強い相関があるので、自然言語の[[埋め込みベクトルをUMAPしてからクラスタリング]]するシチュエーションで同様の振る舞いをすると言えるかどうかは微妙
- と思ってたら2次元にUMAPしてからクラスタリングするのは精度が下がるという研究もあった
    - [[An Empirical Configuration Study of a Common Document Clustering Pipeline]]
- つまり画像系データセットのデータが低次元の多様体の周辺に分布していることによって次元削減のデメリットを受けにくかったのだろう


- [Document embedding using UMAP — umap 0.5.8 documentation](https://umap-learn.readthedocs.io/en/latest/document_embedding.html)
