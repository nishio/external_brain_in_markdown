---
title: "HDBSCAN"
---

> HDBSCAN - Hierarchical Density-Based Spatial Clustering of Applications with Noise. Performs [[DBSCAN]] over varying epsilon values and integrates the result to find a clustering that gives the best stability over epsilon. This allows HDBSCAN to find clusters of varying densities (unlike DBSCAN), and be more robust to parameter selection.
- [scikit-learn-contrib/hdbscan: A high performance implementation of HDBSCAN clustering.](https://github.com/scikit-learn-contrib/hdbscan)
- 異なるepsilonについてのDBSCANを行うため、データの中に密度が異なるクラスターがいる場合によいという話

> HDBSCAN is a clustering algorithm developed by Campello, Moulavi, and Sander. It extends DBSCAN by converting it into a hierarchical clustering algorithm, and then using a technique to extract a flat clustering based in the stability of clusters.
- [How HDBSCAN Works — hdbscan 0.8.1 documentation](https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html)
- DBSCANを[[階層的クラスタリング]]に変換する

色々読んでからこれを再度読むとこれを書いた人がすごくよく理解していい図解をしていることがわかる
- [Understanding HDBSCAN and Density-Based Clustering](https://pberba.github.io/stats/2020/01/17/hdbscan/)
- [[相互到達距離]]の空間における[[凝集型階層的クラスタリング]]([[Single Linkage]])

min_samplesを増やすことは密度推定にスムージングをかける効果がある
- 小さいこぶは消滅する

[[Accelerated Hierarchical Density Clustering]]

Density-based Clustering
[https://findresearcher.sdu.dk/ws/files/171664269/widm.1343.pdf](https://findresearcher.sdu.dk/ws/files/171664269/widm.1343.pdf)
この論文はHDBSCAN*アルゴリズムの高速化手法を提案していますが、特に興味深い点は以下の3つの異なる視点からアルゴリズムを説明していることです:
1. 統計的視点:
    - データは未知の密度関数からサンプリングされていると仮定
    - クラスター木を密度関数のレベルセットから構築
    - [[Robust Single Linkage]]の考え方を拡張
        - > ユークリッド空間で単一リンケージクラスタリングを行うと、ノイズの多いポイントが島を横切る偽の橋を形成する可能性があるため、ノイズの影響を受けやすくなります。点をλ空間に埋め込むことにより、「反発効果」により、クラスタリングがノイズに対してはるかに堅牢になります。 --- [Understanding HDBSCAN and Density-Based Clustering](https://pberba.github.io/stats/2020/01/17/hdbscan/)
2. 計算的視点:
    - DBSCANのパラメータεを全値で探索する階層的拡張として解釈
    - mutual reachability distanceという新しい距離メトリックを導入
        - [[相互到達距離]]([[相互接続距離]])
    - 木の簡略化と安定性スコアに基づくクラスター抽出
3. 位相的視点:
    - 持続的ホモロジーの概念を使用
    - [[シーフ理論]]を用いてクラスター構造を表現
    - 距離スケールにわたる持続性を定式化
これらの3つの視点は、同じアルゴリズムを異なる理論的枠組みで解釈できることを示しており、各分野の研究者にとって理解しやすい説明を提供しています。

特に位相的視点は本論文の新しい貢献であり、これによりマルチパラメトリックな拡張や、より一般的な数学的ツールの適用が可能になることが示唆されています。

この理論的な統合は、HDBSCAN*の理解を深め、さらなる改良への道を開くものとして重要な意義を持っています。また、異なる分野の研究者が協力してアルゴリズムを改善できる基盤を提供しています。


[Understanding HDBSCAN and Density-Based Clustering](https://pberba.github.io/stats/2020/01/17/hdbscan/)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
このブログ記事はHDBSCAN*アルゴリズムの直感的な理解を助けることを目的とした解説です。主なポイントは:
1. HDBSCAN*の基本的な特徴:
    - ノイズを含むデータに対して頑健
    - クラスタの形状や密度に関する仮定が少ない
    - K-meansと違い、事前にクラスタ数を指定する必要がない
2. 密度ベースのクラスタリングの考え方:
    - クラスタを「疎な領域で区切られた密な領域」として定義
    - 確率密度関数(PDF)の山と谷をクラスタとして捉える
    - [[クラスタの持続性]](persistence)で重要性を評価
3. 密度推定の方法:
    - K番目の最近傍点までの距離(core distance)を使用
    - [[mutual reachability distance]]という新しい距離メトリックを導入
    - これにより疎な領域の点が「反発」効果を持つ
4. パラメータ設定:
    - min_samples: PDFの推定の滑らかさを制御
    - min_cluster_size: クラスタの最小サイズを指定し、小さな変動を無視
5. 実装の流れ:
    1. core distanceの計算
    2. mutual reachability distanceに基づく最小全域木の構築
    3. 木の剪定
    4. excess of massによるクラスタの選択

この記事は理論的な説明ではなく、直感的な理解を重視した実践的な解説となっています。特に、視覚的な例を多用してアルゴリズムの動作を説明している点が特徴です。
![image](https://gyazo.com/b6fd678c63a2091e328d92a6ce18bd33/thumb/1000)


[HDBSCANを解説 → Pythonでinstall、実行 #インストール - Qiita](https://qiita.com/ozaki_inu/items/45fb17cd3596a64ed489)



from [[BERTopic: Neural topic modeling with a class-based TF-IDF]]
HDBSCAN
[[BERTopic]]では、HDBSCANアルゴリズムを使って、埋め込み空間上のドキュメントのクラスタリングを行います。これは、BERTopicのトピックモデリングプロセスにおける重要なステップの1つです。

HDBSCANは、Hierarchical Density-Based Spatial Clustering of Applications with Noiseの略で、密度ベースのクラスタリングアルゴリズムです。以下のような特徴があります。

1. 密度の違いを考慮できる
HDBSCANは、密度の違いを考慮してクラスタリングを行うことができます。これにより、密度の高い領域と低い領域を自動的に分離し、よりコンパクトで意味のあるクラスタを見つけることができます。

2. ノイズに頑健
密度の低い領域にある点をノイズとして扱うことができるため、外れ値の影響を受けにくくなります。これは、トピックモデリングにおいて、無関係なドキュメントを適切に扱うために重要な性質です。

3. クラスタ数を指定する必要がない
多くのクラスタリング手法とは異なり、HDBSCANではクラスタ数を事前に指定する必要がありません。これは、最適なトピック数が不明な場合に特に有用です。

4. [[階層的クラスタリング]]が可能
HDBSCANは、クラスタの階層構造を捉えることができます。これにより、トピックの粒度を調整し、より詳細なサブトピックを見つけることができる可能性があります。

BERTopicでは、このHDBSCANアルゴリズムを用いて、埋め込み空間上のドキュメントをクラスタリングし、各クラスタを1つのトピックに対応づけます。これにより、意味的に関連するドキュメントが同じトピックにまとめられ、より解釈可能なトピックモデルが得られます。
HDBSCANの特性を生かすことで、BERTopicは、ノイズに頑健で、密度の違いを考慮した、柔軟なトピック抽出を実現しているのです。
