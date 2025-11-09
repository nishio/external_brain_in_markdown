---
title: "Stop Misusing t-SNE and UMAP for Visual Analytics"
---

[PDF](https://arxiv.org/pdf/2506.08725)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- 論文は「t-SNE/UMAPの誤用が可視化実務で常態化」していることを、136本の論文レビュー＋利用者12名／DR研究者8名インタビューで検証。主因はDRリテラシー不足と「皆が使っているから安全」という思い込み。対策として、タスクに適したDRとハイパラを自動選択する仕組み（仮称 VoyagerDR）も提案。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>DRって何かと思ったらDimension Reductionを略したのかw

![image](https://gyazo.com/bcc6f7e036e7283a11d0e7df449afd83/thumb/1000)
- タスク別：使い分け早見表
    - 識別系（Identification）＝近傍探索・外れ値検出・クラスタ“有無”の把握
        - → [[t-SNE]] / [[UMAP]]（局所構造の可視化に強い）
    - 調査系（Investigation）＝点間距離比較・クラスタ間距離/密度比較・クラス分離度の吟味
        - → [[PCA]] / [[MDS]]や密度・大域に強い派生法（[[densMAP]], [[TriMap]], ほか）
