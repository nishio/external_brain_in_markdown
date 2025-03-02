---
title: "AI各社の機能的棲み分け"
---

2025-02-26
OpenAIがデファクト1位的地位を占めていることに対する各社の戦略

Metaはオープン戦略を取った

Google Geminiは他社より一桁大きいロングコンテキスト路線をとった
- [長いコンテキスト  |  Gemini API  |  Google AI for Developers](https://ai.google.dev/gemini-api/docs/long-context?hl=ja)
- それを活かした [[NotebookLM]]

Anthropicはツール活用が得意になる方向に進化し、[[Prompt Caching]]や、[[AnthropicのMCP]]などのツールエコシステムを発展させる戦略をとってきた
- [[Claude 3.7]]のリリース、同日に[[Devin.ai]]もClaude 3.7にアップデート
- [https://x.com/AnthropicAI/status/1894092430560965029](https://x.com/AnthropicAI/status/1894092430560965029)
- > [cognition_labs](https://x.com/cognition_labs/status/1894125030583537974) 1/ Claude 3.7 Sonnet is live in Devin! The new model is the best we have seen to-date on a variety of tasks including debugging, codebase search, and agentic planning.
- >  ![image](https://gyazo.com/f23f1f3fba7a6b41837702563e72d5e0/thumb/1000)
- 間は3時間ない、一般向け公開と同タイミングで知ってこの速度でプロダクションに入れられるわけがないので、当然情報共有されているわけだ

xAI Grokは他社が取りにくいX(Twitter)のリアルタイム性の高いデータを使うことで、特にイベント後の反響調査などに他ができない強みを持っている
