---
title: "Theanine(記憶システム)"
---

![image](https://gyazo.com/f6a91a90c8f5ee6c94b93e627fb5c743/thumb/1000)

Towards Lifelong Dialogue Agents via [[Timeline-based Memory Management]]
[https://arxiv.org/abs/2406.10996#:~:text=conversations,are%20at%20this%20https%20URL](https://arxiv.org/abs/2406.10996#:~:text=conversations,are%20at%20this%20https%20URL)

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
Theanine (Ong et al., NAACL 2025): 長期対話における[[タイムライン型メモリ管理]]のフレームワークです​。既存研究が不要な古い記憶を破棄することに注力してきたのに対し、Theanineはあえて記憶を削除せず保持し続けます​。
その代わり、各記憶を発生時間や因果関係に基づきリンクし、関連する出来事を因果タイムラインとして構造化します​。
対話応答時には現在の文脈に関連する出来事系列（例えばユーザ行動の変遷）を丸ごと参照し、過去の経緯を踏まえた発話を生成します​。
これにより、一見古い出来事でも「ユーザ行動の変化」という文脈手がかりとして活用し、より一貫性ある応答や長期関係の構築に繋げます​。

また、評価手法としてTeaFarmと呼ぶカウンターファクト（反事実）対話生成に基づくスキームを提案し、過去記憶を統合した応答生成を自動評価する工夫も行っています​。Theanineは長期対話の文脈理解力を高める新しい視点として注目されます。



private prototype
[https://github.com/nishio/private/tree/devin/1742967627-prototype-from-paper](https://github.com/nishio/private/tree/devin/1742967627-prototype-from-paper)
[https://app.devin.ai/sessions/f0a2ea386d10436bb20cb97a02129057](https://app.devin.ai/sessions/f0a2ea386d10436bb20cb97a02129057)
