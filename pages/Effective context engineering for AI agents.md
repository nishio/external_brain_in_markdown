---
title: "Effective context engineering for AI agents"
---

[[Anthropic]]のEngineering blog記事 (2025-09-29)
- [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- 著者: Prithvi Rajasekaran, Ethan Dixon, Carly Ryan, Jeremy Hadfield (Applied AI team)
「プロンプトでタスクを細かく指示しすぎるな」という主張の出典

[[コンテキストエンジニアリング]]
- [[プロンプトエンジニアリング]]の発展形
- 指示文だけでなく、システムプロンプト・ツール・外部データ・会話履歴を含めて、推論時にどのトークンを置くかを整える
- 文脈が長くなると性能が落ちる([[Context Rot]])
    - モデルの注意には予算がある

システムプロンプトは「right altitude」(適切な高度)で書く
- 失敗1: 細かすぎる
    - >  hardcoding complex, brittle logic in their prompts to elicit exact agentic behavior
    - 複雑で壊れやすいロジックをプロンプトにハードコードして、正確な振る舞いを引き出そうとする
- 失敗2: 曖昧すぎる
    - >  vague, high-level guidance that fails to give the LLM concrete signals for desired outputs or falsely assumes shared context
    - 具体的な手がかりを与えない漠然とした指示、または共有されていない前提を共有されていると思い込む
- その中間: 振る舞いを導くだけの具体性と、モデルが自分で判断できる柔軟性を両立させる
- 例示について
    - エッジケースの長いリストを詰め込むな
    - 期待する振る舞いを表す、多様で典型的な例を厳選せよ

指導原理
- >  Find the smallest set of high-signal tokens that maximize the likelihood of your desired outcome.
- 望む結果の確率を最大化する、最小の高シグナルなトークン集合を見つけよ

その他の話題
- ツールは最小限・機能の重なりなく
- just-in-time retrieval: 軽い識別子だけ持ち、必要なときに読み込む
- 長いタスクのために
    - compaction: 上限近くで履歴を要約して作り直す
    - 構造化ノート: エージェントが外部にメモを書き、後で読む
    - サブエージェント: 専門エージェントがきれいな文脈で作業し、主エージェントが束ねる

関連
- [[探索を加速する抽象度の設計勉強会]]で「適切な明確さ」として引用した
    - 自走力の高い人に細かい指示をするのは[[マイクロマネジメント]]で良くない、AIに対しても同じ
    - この「適切な水準」はモデルによって異なる