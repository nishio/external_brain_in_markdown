---
title: "Agentic Retrieval"
---

[[Agentic Search]]と言ってしまうことが多いけど、まだあんまりメジャーな使い方ではないそうだ
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
- 技術的には agentic retrieval や agentic RAG の方が説明しやすいです。
- Microsoft Azure AI Search は “agentic retrieval” を、LLM が複雑な質問をサブクエリに分解し、検索を実行し、結果を統合する仕組みとして説明しています。これは「検索」よりも「検索パイプラインを LLM が制御する」という点が明確です。
    - [Agentic Retrieval Overview - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview?tabs=quickstarts)
- LangChain も “Agentic RAG” を、LLM-powered agent が推論中に「いつ・どのように retrieve するか」を決める方式として整理しています。通常の 2-step RAG では retrieval が生成前に固定的に起きるのに対し、Agentic RAG では agent が必要に応じて retrieval tool を使います。
    - [Retrieval - Docs by LangChain](https://docs.langchain.com/oss/python/langchain/retrieval)
- Claude Skills の仕組みを説明するなら、Anthropic 自身の用語では progressive disclosure が中心です。Skill は SKILL.md を含むディレクトリで、起動時には各 Skill の name と description だけが system prompt に読み込まれ、Claude が関連すると判断した場合に SKILL.md 本文を読み、さらに必要なら追加ファイルを読む、という構造です。
    - この場合、実際に起きているのは古典的な「検索」というより「Markdown の軽量メタデータを目次・索引として見せ、agent が状況に応じて読むべき本文や参照ファイルを選ぶ」という仕組みです。
    - [Equipping agents for the real world with Agent Skills \ Anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

[[Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG]]
- [[Agentic RAG]]
