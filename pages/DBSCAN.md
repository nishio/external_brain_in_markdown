---
title: "DBSCAN"
---

これの階層化バージョンが[[HDBSCAN]](処理速度は重くなるがパラメータ調整が楽になる)

Martin Ester, Hans-Peter Kriegel, Jörg Sander, and Xiaowei Xu. 1996. A density-based algorithm for discovering
clusters in large spatial databases with noise. In Proceedings of the 2nd ACM International Conference on Knowledge
Discovery and Data Mining (KDD). 226–231.
[A density-based algorithm for discovering clusters in large spatial databases with noise | Proceedings of the Second International Conference on Knowledge Discovery and Data Mining](https://dl.acm.org/doi/10.5555/3001460.3001507) [PDF](https://cdn.aaai.org/KDD/1996/KDD96-037.pdf)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
これは1996年のKDD会議で発表されたDBSCAN(Density-Based Spatial Clustering of Applications with Noise)アルゴリズムの原論文です。主なポイントは:
1. DBSCANの特徴と利点:
    - 密度ベースのクラスタリング手法で、任意の形状のクラスタを発見可能
    - ノイズ(外れ値)を自然に検出できる
    - 入力パラメータが少なく(Eps, MinPtsの2つのみ)、パラメータの選択も比較的容易
    - 大規模空間データベースに対して効率的
2. アルゴリズムの仕組み:
    - [[密度到達可能性]](density-reachability)と[[密度連結性]](density-connectivity)の概念を導入
        - ![image](https://gyazo.com/d228d417eb0cec4c9667370d240d6479/thumb/1000)
        - ![image](https://gyazo.com/e740ae1593f3ce3cd65ebbfd52675512/thumb/1000)
    - コアポイント、ボーダーポイント、ノイズポイントという3種類の点を定義
        - ![image](https://gyazo.com/76bef8d81d00751e6c47a594aa85d0d2/thumb/1000)
    - R*-treeなどの空間インデックスを利用して効率的に近傍点を探索
3. 性能評価:
    - 当時の代表的なクラスタリング手法CLARANSと比較
    - 任意形状のクラスタ発見において優れた精度を示す
    - 実行時間はCLARANSの100倍以上高速
4. パラメータ設定:
    - MinPtsは通常4に設定(2次元データの場合)
    - Epsはk-dist plotというグラフを用いて対話的に決定
        - ![image](https://gyazo.com/1313cec66e1f5e7a0bd95d1721cb6ec9/thumb/1000)

この論文はDBSCANの基礎となる重要な論文で、密度ベースクラスタリングの分野に大きな影響を与えました。2014年にはSIGKDD Test of Time Awardを受賞しています。