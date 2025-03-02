---
title: "Polis"
---

> Polisは高度な統計学と機械学習により、大勢の人々が自分の言葉で何を考えているかを収集、分析、理解するためのリアルタイム・システムです。(DeepL)
- [Polis | The Computational Democracy Project](https://compdemocracy.org/Polis/)
- [[Pol.is]]ともよく表記されてるが、本家が自分のことをPolisと呼んでるのでそうした
- [[意見分布の可視化]]

<img src='https://scrapbox.io/api/pages/nishio/nihia/icon' alt='nihia.icon' height="19.5"/>Polis（ポリス）とは、多数の人々の意見や感情を収集し、リアルタイムに分析するシステムです。このシステムは、高度な統計学と機械学習を利用して、集められた意見を理解しやすくすることを目指しています。
- 主な特徴
    - リアルタイム収集と分析: 大勢の人々の意見をリアルタイムで収集し、分析することで、現在の意見動向を把握できます。
    - 効率的な意見収集: アンケート調査よりも有機的で、フォーカスグループよりも労力を必要としないように設計されています。
    - クラスター分析: 集められた意見をクラスター分析し、共通の意見や対立する意見を明確にします。これにより、多様な意見の全体像を理解できます。
- 主な用途
    - 政策決定: 政府や企業が市民や顧客の意見を収集し、政策やサービスの改善に役立てることができます。
    - コミュニティの合意形成: コミュニティ内での意見調整や合意形成をスムーズに行うために利用されます。
- 技術的背景
    - Polisは、主に以下の技術を使用しています。
        - 次元削減: PCA（主成分分析）やUMAPなどを使用して、高次元データを低次元に削減し、視覚的に理解しやすくします。
        - クラスター分析: K-Means法やLeidenアルゴリズムを用いて、意見をクラスター化し、共通の意見群を抽出します。

これがとても参考になる
- [https://github.com/compdemocracy/analysis-python/blob/main/notebooks/american-assembly-specific/american-assembly-representative-groups-and-comments.ipynb](https://github.com/compdemocracy/analysis-python/blob/main/notebooks/american-assembly-specific/american-assembly-representative-groups-and-comments.ipynb)
- <img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>このコードは、参加者がコメント（発言）に対して「賛成(+1)」「反対(-1)」「未投票(0)」したデータを用いて、意見空間を可視化・クラスタリングする一連の手順を示しています。
    - 主な処理は以下のとおりです：
        - データの前処理：
            - データ読み込み・欠損値処理・投票数のしきい値に基づく参加者フィルタリング
            - 適切なコメント（モデレーション後も残ったもの）の抽出
        - 次元削減 (PCA)：
            - 投票行列を主成分分析(PCA)で低次元(2次元)に圧縮し、参加者を2次元空間上にプロット。
        - クラスタリング (K-means)：
            - まずPCA結果を用いて参加者を細かく100クラスタに分類し、その後、その100クラスタの中心をさらに2～5クラスタでまとめ、シルエットスコアにより最適なクラスター数を選択。
        - 代表的コメントの抽出：
            - 各グループで特に特徴的なコメントを[[Fisherの正確検定]]と比率R_v(g,c)を用いて抽出し、それぞれのグループ特有の意見傾向を示すコメントを特定。
    - 要約すると、このコードは多数の参加者とコメントからなる投票データに対して、次元削減やクラスタリングを行い、意見グループを導出し、そのグループの特徴を代表するコメントを定量的に特定するまでの一連の分析手順を示しています。


[[Polis: Scaling Deliberation by Mapping High Dimensional Opinion Spaces]]
[[Polis勉強会]]


[https://github.com/compdemocracy/polis](https://github.com/compdemocracy/polis)
[https://github.com/pol-is](https://github.com/pol-is)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>試してみたもの
- [[Polis体験レポート:テロの原因究明をするか]]
- [[Polis体験レポート:同性婚を合法化すべきか]]



<img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/>
- Polisプロジェクトは、アンケート調査よりも有機的で、フォーカスグループよりも労力を必要としないように設計された、AIを活用した[[感情収集プラットフォーム]]です。理解されたいという人間の基本的な欲求をスケールアップして満たすことを目的としています。
    - > Polis is an AI powered [[sentiment gathering]] platform.
        - [[sentiment gathering platform]] という表現をしている<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - [[理解されたいという欲求]]
        - > the basic human need to be understood



[[西尾の体験 on Plurality Tokyo]]

# [Algorithms](https://compdemocracy.org/algorithms/)
- Dimensionality reduction
    - [[PCA]]
    - [[UMAP]]
- Clustering
    - [[K-Means]]
    - [[Leiden graph based community detection]]
    - [[Hierarchical clustering]]




> [@nishio](https://twitter.com/nishio/status/1645979580623355904): Polisの良いところは[[短文]]であるところかも。人間が機械の支援なしに100人と合意形成しようとすると、自分が書いた文章の100倍の量を読まないといけないのだが、大部分の人間はそれに耐えられない。自分の意見に近い意見は理解しやすく、遠い意見は理解しにくいので近い意見を多く感じる

[[Polisをもっとやりたい]]
