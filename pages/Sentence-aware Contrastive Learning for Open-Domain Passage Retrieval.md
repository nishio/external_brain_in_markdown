---
title: "Sentence-aware Contrastive Learning for Open-Domain Passage Retrieval"
---

> Training dense passage representations via contrastive learning has been shown effective for Open-Domain Passage Retrieval (ODPR). Existing studies focus on further optimizing by improving negative sampling strategy or extra pretraining. However, these studies keep unknown in capturing passage with internal representation conflicts from improper modeling granularity. Specifically, under our observation that a passage can be organized by multiple semantically different sentences, modeling such a passage as a unified dense vector is not optimal. This work thus presents a refined model on the basis of a smaller granularity, contextual sentences, to alleviate the concerned conflicts. In detail, we introduce an in-passage negative sampling strategy to encourage a diverse generation of sentence representations within the same passage. Experiments on three benchmark datasets verify the efficacy of our method, especially on datasets where conflicts are severe. Extensive experiments further present good transferability of our method across datasets.
[https://aclanthology.org/2022.acl-long.76/](https://aclanthology.org/2022.acl-long.76/)
- (DeepL) 対照学習による密なパッセージ表現の訓練は、ODPR（Open-Domain Passage Retrieval）に有効であることが示されている。既存の研究では、ネガティブサンプリング戦略の改善や追加的な事前学習により、さらなる最適化を行うことに焦点が当てられている。しかし、これらの研究では、不適切なモデリングの粒度に起因する、内部表現の衝突を持つパッセージを捕捉することは困難である。具体的には、1つの文章が複数の意味的に異なる文によって構成され得るという我々の観測の下では、そのような文章を統一された密なベクトルとしてモデル化することは最適ではない。そこで本研究では、より小さな粒度である文脈文に基づく洗練されたモデルを提示し、懸念される競合を緩和する。詳細には、同じパッセージ内の文表現の多様な生成を促すために、パッセージ内ネガティブサンプリング戦略を導入する。3つのベンチマークデータセットを用いた実験により、特に競合が激しいデータセットにおいて、本手法の有効性を検証する。さらに、広範な実験により、本手法がデータセット間で良好な移植性を持つことを示す。

検索対象の単位が適切でないことによって問題が起きる、もっと細かく刻むことで解決する、という話
- ![image](https://gyazo.com/9eb9b2ec68bea2cdbe4be0127a2da199/thumb/1000)
- ではどう刻むか？
    - 文章区切りに特殊トークンを入れてBERTでそのトークンのタイミングの出力を取る
    - 正解文とそれ以外、および不正解文章との間の[[Contrastive Learning]]をする
    - なるほどなー、入力の文字列自体を分割してしまうと文脈がわからなくなってしまう、この方法なら共通の文脈を踏まえて文ごとの埋め込みができる
