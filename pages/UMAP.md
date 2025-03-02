---
title: "UMAP"
---

[[2022年参院選のUMAP可視化]]の文脈でのQ&A
- Q: UMAPとは？PCAとはどう違う？
- A:
    - [[PCA]]は高次元のものをぐるぐる回して一番広がってる方向から観察しようというもの
    - 観察対象が[[世論地図]]の場合多くても10次元前後なのに対し[[東京大学谷口研究室・朝日新聞社共同調査]]データは42次元なので「どこからみても奥行方向に割と厚みがあって無理…」となりがち
    - UMAP(に限らず非線形の[[次元削減]]手法)は観察対象にゴム膜のようなものを押し付けてなるべくうまいこと形を写し取ろうとするようなもの
    - 膜は曲がるので縦軸横軸には意味がなくなる一方、観察対象によってはPCAよりきれいに構造を写し取れる
    - UMAPは2018年に出てきた、非線形手法の中では新しめのもので、[[Talk to the City]]も中で使っている。


UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction
Leland McInnes, John Healy, James Melville
UMAP (Uniform Manifold Approximation and Projection) is a novel manifold learning technique for dimension reduction. UMAP is constructed from a theoretical framework based in Riemannian geometry and algebraic topology. The result is a practical scalable algorithm that applies to real world data. The UMAP algorithm is competitive with [[t-SNE]] for visualization quality, and arguably preserves more of the global structure with superior run time performance. Furthermore, UMAP has no computational restrictions on embedding dimension, making it viable as a general purpose dimension reduction technique for machine learning.
[https://arxiv.org/abs/1802.03426](https://arxiv.org/abs/1802.03426)

[UMAP: Uniform Manifold Approximation and Projection for Dimension Reduction — umap 0.5 documentation](https://umap-learn.readthedocs.io/en/latest/)

[Understanding UMAP](https://pair-code.github.io/understanding-umap/)

[https://qiita.com/odanny/items/06ab88353bcee7bf6aa7](https://qiita.com/odanny/items/06ab88353bcee7bf6aa7)

from [[BERTopic: Neural topic modeling with a class-based TF-IDF]]
UMAP
UMAPは、Uniform Manifold Approximation and Projectionの略で、高次元データを低次元空間に埋め込むための次元削減手法です。[[BERTopic]]では、このUMAPを使って、高次元のドキュメント埋め込みをクラスタリングに適した低次元空間に変換します。

UMAPには以下のような特徴があります。

1. 非線形次元削減
UMAPは、非線形の次元削減が可能で、データの局所的な構造と大域的な構造の両方を保持することができます。これにより、より忠実にデータの本質的な構造を低次元空間で表現できます。

2. 柔軟性が高い
UMAPには、近傍グラフの構築方法やコストファンクションなど、いくつかのハイパーパラメータがあります。これらを調整することで、データの特性に応じた最適な埋め込みを得ることができます。

3. スケーラビリティ
UMAPは、大規模データセットに対しても効率的に動作します。これは、トピックモデリングのように大量のドキュメントを扱う場合に重要な性質です。

4. 確率的な解釈
UMAPの埋め込みは、確率的な解釈を持ちます。これにより、埋め込み空間上の距離が、データ点間の類似度を反映していると考えることができます。

BERTopicでは、ドキュメントをBERTなどの言語モデルで高次元ベクトルに埋め込んだ後、UMAPを用いて低次元空間に射影します。この低次元空間上でHDBSCANを適用することで、効率的かつ効果的なクラスタリングが可能になります。

UMAPの非線形性とスケーラビリティを利用することで、BERTopicは大規模でノイズの多いデータセットに対しても、意味のあるトピックを抽出することができるのです。また、UMAPのパラメータを調整することで、トピックの粒度をある程度制御することも可能になります。

以上のように、UMAPはBERTopicにおける重要な前処理ステップであり、高次元のドキュメント埋め込みを、クラスタリングに適した形に変換する役割を果たしています。
