---
title: "SybilRank"
---

[[ソーシャルグラフ]]で[[人間性の証明]]

[[Aiding the Detection of Fake Accounts in Large Scale Social Online Services]]
- > We introduce a new tool in the hands of OSN operators, which we call SybilRank . It relies on social graph properties to rank users according to their perceived likelihood of being fake (Sybils). SybilRank is computationally efficient and can scale to graphs with hundreds of millions of nodes, as demonstrated by our Hadoop prototype. We deployed SybilRank in Tuenti’s operation center. We found that ∼90% of the 200K accounts that SybilRank designated as most likely to be fake, actually warranted suspension. On the other hand, with Tuenti’s current user-report-based approach only ∼5% of the inspected accounts are indeed fake.
- ![image](https://gyazo.com/cdc9b35a99ccc5919bdb81c4ffd7dd33/thumb/1000)
- [https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final42_2.pdf](https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final42_2.pdf)
- (DeepL) 我々は、OSNオペレータの手になる新しいツール、SybilRankと呼ぶものを紹介する。このツールは、ソーシャルグラフの特性を利用して、ユーザーを偽者（Sybils）である可能性の高さに応じてランク付けするものである。SybilRankは計算効率が高く、Hadoopプロトタイプで実証されたように、数億のノードを持つグラフに拡張可能です。我々はSybilRankをTuentiのオペレーションセンターに配備しました。その結果、SybilRankが偽物の可能性が高いと判断した20万件のアカウントのうち、約90%が実際に停止を余儀なくされることがわかりました。一方、Tuentiの現在のユーザーレポートベースのアプローチでは、検査されたアカウントのうち約5%しか本当に偽のアカウントではありませんでした。

from [[オモイカネ勉強会]]
- ([[World ID]]は)「IDに基づく重要な課題」として「個人のユニークな[[人間性の証明]]」を挙げている
- 例えば[[SybilRank]]
    - > ソーシャルグラフの特性を利用して、ユーザーを偽者（Sybils）である可能性の高さに応じてランク付けするものである。SybilRankは計算効率が高く...数億のノードを持つグラフに拡張可能
    - ![image](https://gyazo.com/cdc9b35a99ccc5919bdb81c4ffd7dd33/thumb/1000)
    - "[[Trust Seeds]]"と呼ばれる信頼度の高いアカウントから信頼が伝搬するアルゴリズム
    - 「網膜スキャンと対応づいたアカウント」は信頼度高い"Trust Seeds"になりうるわけ

