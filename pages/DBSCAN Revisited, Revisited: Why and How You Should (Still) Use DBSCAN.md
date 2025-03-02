---
title: "DBSCAN Revisited, Revisited: Why and How You Should (Still) Use DBSCAN"
---

[DBSCAN Revisited, Revisited: Why and How You Should (Still) Use DBSCAN: ACM Transactions on Database Systems: Vol 42, No 3](https://dl.acm.org/doi/abs/10.1145/3068335)
[PDF](https://www.khoury.northeastern.edu/home/vip/teach/DMcourse/2_cluster_EM_mixt/notes_slides/revisitofrevisitDBSCAN.pdf)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
この論文は2015年のSIGMODで発表された「DBSCAN Revisited」への反論を行っています。主な論点は以下の通りです:
1. DBSCANの理論的な実行時間の限界について:
    - SIGMODの論文はDBSCANがO(n log n)で実行できないことを証明したが、それは実用上「計算困難」という意味ではない
    - 多くの代替手法がΘ(n²)やΘ(n³)である中で、DBSCANは依然として大規模データでも有効な手法である

2. 実験の問題点:
    - SIGMODの論文で使用されたパラメータ(特にε)が不適切に大きすぎた
    - より適切な小さいεを使用すると、インデックスを活用した元のDBSCANの方が高速に動作することを示した
    - データセットの前処理が不適切で、有意なクラスタリング結果が得られていない

3. DBSCANの利点:
    - ユークリッド距離以外の距離関数も使用可能
    - R*-treeなど様々なインデックス構造と組み合わせ可能
    - 実際のアプリケーションで効率的に動作する

結論として、SIGMODの論文は理論的な下界を示した点では価値があるものの、「DBSCANは大規模データで使用すべきでない」という主張は適切ではなく、適切なパラメータとインデックスを使用すれば、DBSCANは依然として競争力のあるアルゴリズムであると主張しています。