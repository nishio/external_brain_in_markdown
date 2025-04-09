---
title: "なぜAzure OpenAI Serviceか"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>OpenAIのAPIを叩くのはダメで[[Azure OpenAI Service]]ならOKという組織は何が判断の理由？

<img src='https://scrapbox.io/api/pages/nishio/GPT-4.5/icon' alt='GPT-4.5.icon' height="19.5"/>主な理由は以下の通りです。

セキュリティ要件の違い
- Azure OpenAI Serviceは[[Microsoft Azure基盤]]上で動作し、データの管理や[[セキュリティポリシー]]をAzure上で統合的に管理できます。これにより、組織のセキュリティ要件を満たしやすくなります。

データの所在地域の制御
- Azureの場合、データを特定の[[リージョン]]に限定できるため、[[GDPR]]やその他規制要件を満たしやすくなります。OpenAIの直接APIはデータ管理地域の指定が困難です。

コンプライアンスと規制準拠
- Azureは各種[[コンプライアンス]]（[[ISO 27001]], [[SOC 2]], [[HIPAA]], [[FedRAMP]]等）に対応しており、コンプライアンス監査や規制要件を満たすことが可能です。

契約上の安定性とサポート体制
- Microsoftとの企業向け契約（Enterprise Agreement）がすでにある場合、Azure経由の契約のほうが法務面での調整が容易です。また、サポート体制が明確になる利点があります。

以上の理由で、組織としてはAzure OpenAI Serviceの利用を許容し、OpenAIの直接API利用は制限することがあります。