---
title: "LLM APIのタイムアウト対策"
---

「タイムアウトする可能性があるLLM APIを叩くサービスの設計としてどんな方法がいいかを検索してまとめて」と言ったら、想像以上に壮大な話をされた

<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>
- 非同期処理とキューの利用
    - API呼び出しを非同期化し、[[RabbitMQ]]や[[Kafka]]などのキューでリクエストを順次処理。

- タイムアウトとリトライ戦略
    - 適切なタイムアウト値を設定し、[[指数バックオフ]]方式でリトライ実施。

- [[サーキットブレーカーパターン]]の導入
    - 一定回数の失敗で呼び出しを中断し、定期チェックで復帰判断。

- キャッシュと状態管理
    - [[Redis]]等でキャッシュを活用し、[[DynamoDB]]などでサーキット状態を管理。

- オーケストレーションと監視
    - [[AWS Step Functions]]などでワークフロー制御、詳細なログと監視で障害対応を強化。

[https://chatgpt.com/c/67c01f64-8c18-8011-8342-ab59b1e75354](https://chatgpt.com/c/67c01f64-8c18-8011-8342-ab59b1e75354)

Redisサーバの立て方
[https://chatgpt.com/c/67c016af-17d0-8011-8dd5-f1cc245b8971](https://chatgpt.com/c/67c016af-17d0-8011-8dd5-f1cc245b8971)

