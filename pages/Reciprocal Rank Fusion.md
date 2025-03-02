---
title: "Reciprocal Rank Fusion"
---

[Reciprocal rank fusion | Elasticsearch Guide 8.13 | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/rrf.html)
$score_i = {1\over a_i} + {1\over b_i}$
- 大小関係としては[[調和平均]]と同じ
- $k$を加えることもある
    - ![image](https://gyazo.com/7fd3a17c5cc500f57a9a380e421765a1/thumb/1000)
        - [Reciprocal Rank Fusion outperforms Condorcet and individual Rank Learning Methods](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf)(PDF)
        - ここではk=60
    - kを増やすと1位と2位の差が小さくなる
