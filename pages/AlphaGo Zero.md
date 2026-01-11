---
title: "AlphaGo Zero"
---

[[AlphaGo]]とは別物
- 人間の記譜データを使わない

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
学習データの違い
- AlphaGo
    - 人間のプロ棋士の棋譜で教師あり学習
    - その後、自己対戦で強化学習
- AlphaGo Zero
    - 棋譜を一切使わない
    - ルールだけを与え、自己対戦のみで学習

モデル構成の違い
- AlphaGo
    - 方策ネットワーク（Policy）
    - 価値ネットワーク（Value）
    - さらに高速なロールアウトなど複数要素
- AlphaGo Zero
    - 単一のニューラルネットが
        - 次の一手の確率（方策）
        - 勝率（価値）
    - を同時に出力
