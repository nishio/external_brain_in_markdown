---
title: "LiteLLM Proxy"
---

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>LiteLLM Proxyは、100種類以上の大規模言語モデル（LLM）のAPIを、OpenAIフォーマットの統一インターフェースで呼び出せるプロキシサーバーです。これにより、Azure OpenAI、Anthropic、Bedrock、HuggingFaceなど複数のプロバイダーのモデルを、1つのAPI経由で利用できるため、コードの統一性や運用効率が向上します。また、エラーハンドリングやフォールバック、キャッシュ、トークン使用量・コストのトラッキング、レートリミット設定など、運用上の便利な機能も備えています。Dockerなどで簡単にデプロイでき、Langfuseなどの観測ツールと連携することで、ログ管理や解析も容易になります。
- [LiteLLM Proxy Server (LLM Gateway) | liteLLM](https://docs.litellm.ai/docs/simple_proxy)
- [BerriAI/liteLLM-proxy](https://github.com/BerriAI/liteLLM-proxy)
