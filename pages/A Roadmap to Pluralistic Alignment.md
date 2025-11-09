---
title: "A Roadmap to Pluralistic Alignment"
---

[A Roadmap to Pluralistic Alignment](https://arxiv.org/abs/2402.05070v1?utm_source=chatgpt.com)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>論文の目的
- LLM を例に「多元的（pluralistic）アラインメント」を実現・評価するための概念枠組みと研究課題を整理し、従来の RLHF 等が抱える限界を指摘する。

なぜ多元性が必要か
- 利用者の多様性：平均的好みへの最適化では[[少数派の価値観がノイズ扱いされる]]。
- カスタマイズ性：安全ガードレール内での細かな調整には、どの価値軸を操作できるかが明示的である必要。
- 技術的利点：多元的モデルは決定根拠が明確になり、解釈性が向上。
- 社会的価値：多価値の共存は多くの民主社会で目指すべき目標そのもの。

[[多元的モデルの3類型]]
[[多元的ベンチマークの3類型]]

現行アラインメントとの関係・実証結果
- 仮説：標準 RLHF は分布的多元性を縮減しうる。
- 実験：LLaMA/LLaMA-2/GPT-3 系で前訓練モデルと RLHF 後モデルを比較すると、前者のほうが人間回答分布（米国・日本など）に近くエントロピーも高い。
    - Jensen-Shannon 距離が小さく、平均エントロピーは約2倍。
- 示唆：現行手法では少数派意見が失われやすく、新たな評価・学習法が必要。

[[RLHF]]は[[分布的多元性]]を減らしてしまうということ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
