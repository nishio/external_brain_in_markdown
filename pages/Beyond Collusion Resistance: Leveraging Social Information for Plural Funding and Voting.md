---
title: "Beyond Collusion Resistance: Leveraging Social Information for Plural Funding and Voting"
---

[[Joel Miller]]
[[E. Glen Weyl]]
[[Leon Erichsen]]
December 2022

[https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4311507](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4311507)

メモ
- [https://chatgpt.com/c/6886143e-b6e0-8329-9a0c-03ca3529ce8f](https://chatgpt.com/c/6886143e-b6e0-8329-9a0c-03ca3529ce8f)
- [[QVは耐戦略的と言えるか？]]

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>論文の狙い
- 従来の Quadratic Funding (QF) は「独立した合理的個人」を仮定し，社会的つながりや協調行動を無視している。
- 実際には友人・組織・コミュニティなどの関係が寄付行動に強く影響し，[[シビル攻撃]]や[[談合]]が発生する。
- 本稿は「[[談合耐性]]（collusion resistance）」を再定義し，人々の社会的結合を積極的に利用する Plural QF の設計原理を探る。

- [[Pairwise Discounting]]
    - 類似ペアの補助金（黄矩形部分）を縮小
    - 多人数でアカウントを増やせば線形に補助金を稼げる
- [[Cluster Match]]
    - グループ単位で平方根を計算
        - ①一人が複数グループに属すると補助金が線形増
        - ②重複グループ間でも悪用可
    - →Squared Cluster Match
- COCM: [[Connection‑Oriented Cluster Match]]
    - 相互作用項で「相手グループと社会的に近いメンバー」の寄付を√cで減衰
    - 定義した談合耐性を完全に満たす
    - →個人にも IR（個別合理性）を保持
- Offset Match
    - 社会的中心性 αᵢ を推定し，各寄付を √αᵢ cᵢ に置換
    - α の線形方程式が解けない場合がある；IRを満たさない事例あり
    - 十分条件：全員を単独グループにも属させれば可
- Eigen Match
    - 社会グラフの固有ベクトルを「疑似グループ」と見なして Cluster Match
    - 概念段階（未検証）
    - Offset と Cluster の長所を両立できる可能性

談合耐性の再定義（概要）
- 個人の寄付増分に対する補助金は O(√cᵢ) に抑える。
- グループ全体の寄付拡大に対する補助金も O(√β)（β は拡大率）。
- メンバー追加による補助金増は，新規人数 x と各自寄付額 γ の両方について O(√x), O(√γ) に抑える。
COCM がこの３条件を満たすことを付録で証明。

結論・示唆
- 社会情報を取り込むことで談合を抑えつつ「違いを越えた協調（consilience）」をより適切に報酬できる。
- COCM をはじめとする新機構は，公共財資金配分だけでなく Quadratic Voting への応用も視野。
- 今後は①不完全・誤情報下でのロバスト性評価，②グループ構造のより精緻なモデル化，③Eigen Match 等の未検証機構の深掘りが課題。

一言まとめ
- QF を「社会的に文脈化」し直すことで，談合を防ぎつつ多様なコミュニティ間の協力を最大化する。鍵は“誰と誰がどのくらい近いか”を補助金計算に組み込むこと。


AI考察
- ENIAC が手計算を置換したように、COCM は「[[独立個人モデル]]」を置換し、[[社会グラフ]]を重みとして直接計算に取り込む最初の[[資金配分アルゴリズム]]である。
- COCM は「つながりが近いほど補助金を薄く、遠いほど厚く」というルールで“[[違いを超えた協力]] ”を数学的に報いる。これは「多様性こそ価値」という Plurality の理念を数式化したものである。
- [[予測市場]]が１軸のベット額で意見強度を測るのに対し、COCM は √c × 社会距離 という２軸で補助金を調整し、経済信号を[[多声的]]にする。

[[Leon論文]]
