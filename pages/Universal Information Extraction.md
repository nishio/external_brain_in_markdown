---
title: "Universal Information Extraction"
---

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
Universal Information Extraction ([[UIE]]) は、単一の言語モデルを用いて複数の情報抽出タスクを統一的に解く方法論です。UIEは2022年のACL論文で提案されました。

UIEの主な特徴は以下の通りです:
- 様々な情報抽出タスク(固有表現抽出、関係抽出、イベント抽出など)を、spotとasocという2つの操作の組み合わせで統一的に表現する。
- spotは文中から対象となる部分(エンティティ等)を抽出する操作、asocはspot間の関係を抽出する操作を表す。
- 抽出結果は構造化された形式(ストラクチャードエクストラクションラングエッジ, SEL)で出力される。
- 1つの言語モデル(論文ではT5やBARTなどの事前学習モデル)だけで全てのタスクを解く。

UIEの利点としては、1つのモデルで様々なタスクが解けるためモデルの管理が容易なこと、タスク間で知識の共有ができること、少ないデータでも学習できることなどが挙げられています。

UIEは事前学習済みの言語モデルと組み合わせることで更に発展しており、情報抽出タスクにおける言語モデル活用の先駆的な研究と言えます。情報抽出の統一的な枠組みとして注目されている手法です。

これかな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
[Unified Structure Generation for Universal Information Extraction - ACL Anthology](https://aclanthology.org/2022.acl-long.395/)
