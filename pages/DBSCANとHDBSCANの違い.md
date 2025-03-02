---
title: "DBSCANとHDBSCANの違い"
---

[[DBSCAN]]と[[HDBSCAN]]の違い
- 簡単に言えばHDBSCANはDBSCANのepsの値を自動調整する仕組み
- 実際のデータで実験して振る舞いを観察する

![image](https://gyazo.com/b33420c5a98cd016a3eebd26a505ddbe/thumb/1000) ![image](https://gyazo.com/656733acc1eb23cd794e535f551d0786/thumb/1000)
[https://pberba.github.io/stats/2020/01/17/hdbscan/](https://pberba.github.io/stats/2020/01/17/hdbscan/)
HDBSCANのデフォルトのクラスタ選択基準であるeom([[Excess of Mass]])の図解


2024-11-14
![image](https://gyazo.com/ff7c969a58a1b63a88fc375355dab761/thumb/1000)
- 左下
    - HDBSCANではパラメータによらず左下の「はっきり分かれてるクラスタ」は全体をクラスタとして認識している
    - DBSCANでは末端部をノイズとして無視しており、パラメータの変化によってだんだん小さくなり、最終的に全部ノイズと判定している
- 右
    - 振る舞いに大差ないがHDBSCANの方が周囲のノイズをクラスタの一部だと判断して巻き込んでしまうことが多いね

[DBSCAN — scikit-learn 1.5.2 documentation](https://scikit-learn.org/1.5/modules/generated/sklearn.cluster.DBSCAN.html)
[[DBSCAN Revisited, Revisited: Why and How You Should (Still) Use DBSCAN]]

[HDBSCAN — scikit-learn 1.5.2 documentation](https://scikit-learn.org/1.5/modules/generated/sklearn.cluster.HDBSCAN.html)
[https://note.com/navy_azalea/n/na859d7ab6ab3](https://note.com/navy_azalea/n/na859d7ab6ab3)
[[相互到達距離]]

[SpectralClustering — scikit-learn 1.5.2 documentation](https://scikit-learn.org/1.5/modules/generated/sklearn.cluster.SpectralClustering.html)
