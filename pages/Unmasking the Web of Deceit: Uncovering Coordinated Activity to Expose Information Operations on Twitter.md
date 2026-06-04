---
title: "Unmasking the Web of Deceit: Uncovering Coordinated Activity to Expose Information Operations on Twitter"
---

[Unmasking the Web of Deceit: Uncovering Coordinated Activity to Expose Information Operations on Twitter](https://ar5iv.labs.arxiv.org/html/2310.09884)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
これは「Twitter上の情報操作（IO: Information Operations）で、協調して動く“中核アカウント（IO drivers）”をどう見つけるか」を、行動の類似度ネットワークで攻めた論文です。

何をした論文？
- ポイントは2つです。
    1. まず、ユーザ同士が「同じことをしている度合い」を使って類似度グラフ（similarity network）を作る
- 行動トレースとして 5種類を使います：
    - Co-Retweet（同じ投稿をRT）
    - Co-URL（同じURLを共有）
    - Hashtag Sequence（同じ順序のハッシュタグ列）
    - Fast Retweet（同じ相手を素早くRT）
    - Text Similarity（内容の類似）
2. そのグラフから「IOの中核」を取り出す方法として、従来のエッジ閾値カットより、中心性でノードを刈り込むほうが安定して強い、という主張です。

なぜ「エッジの重みで切る」だけだとダメ？
従来は「類似度が高いエッジだけ残す（高い閾値でフィルタ）」で“怪しい塊”を出すことが多かった。
でもこの論文は、IOによって効く行動トレースが違うので、閾値フィルタがキャンペーン間で安定しないと示します。 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))

提案1：中心性ベースの「ノード刈り込み（node pruning）」
発想はシンプルで、
- IOの中核は「誰か1人と超似てる」より、**“多人数とそこそこ似てる”**が起きがち
- だから エッジ重みより **ノード中心性（degree/eigenvector等）**が効く
- 中心性が高いノードをIO driverとして拾う（閾値で刈る） ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
結果：エッジフィルタからノード刈り込みへ切り替えると、平均でprecisionが大きく改善（論文中では平均+0.42の改善と記述）。 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))

提案2：複数トレースを「融合（fused network）」する
各トレースで別々に作った類似度ネットワークを統合します。
論文中で一番効いた融合はかなり割り切っていて、**「どれか1つでも繋がってたら fused でも繋ぐ」**というOR結合に近い形。 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
この fused network を中心性で刈るだけでも、平均AUC/F1が良い（例：AUC≈0.83, F1≈0.76 と要約）。 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))

提案3：埋め込み + 教師あり分類（グローバル検知・将来予測）
さらに fused network を node2vec などのノード埋め込みで 128次元ベクトルにして、Random Forestで分類します（10-fold CV）。 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
- (Task1) IOごとに検知：平均で precision 0.96 / AUC 0.94 / F1 0.82 と報告 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
- (Task2) 複数国IOを混ぜた“グローバル”分類でも precision 0.95 程度 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
- (Task3) 過去年までで学習し、将来IOに関わるユーザを予測：年が進むほど改善し、高precisionを維持した、という主張 ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))

この論文の「あなたの用途（同期投稿→FIMI/IO検知）」への刺さり方
西尾さんの関心（同期投稿タイミングのシグナル化）に直結するのは：
- Fast Retweetや同期系は“単発の強い一致”より、**ネットワーク中心に浮く「中核」**を拾うのが強い、という示唆
- 同期投稿（時間）だけに寄せるとキャンペーン差で外すので、URL共有・共通RT・ハッシュタグ列なども足して fuse すると頑健になる ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))
- まずは教師なし（中心性刈り込み）で候補を出し、ラベルが作れるなら埋め込み+RFへ、という段階設計がそのまま再現実験の形になります ([ar5iv](https://ar5iv.labs.arxiv.org/html/2310.09884))

必要なら、この論文流で「日本の選挙期間Twitter + CN（Community Notes）でやる」再現手順を、あなたのデータ前提（どの粒度でログがあるか）に合わせて**実験プロトコル（特徴量定義→グラフ構築→融合→中心性→評価）**まで落として書けます。

