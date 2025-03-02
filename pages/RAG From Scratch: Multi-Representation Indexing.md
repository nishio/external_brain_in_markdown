---
title: "RAG From Scratch: Multi-Representation Indexing"
---

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
- [[RAG From Scratch]]ビデオシリーズでは、RAGの重要な概念を短く焦点を絞ったビデオでコード付きで解説している。
- 第12回目のビデオでは、ドキュメント全体のインデックス作成に役立つトリックにフォーカスしている。
- 多くのRAGアプローチは、ドキュメントをチャンクに分割し、入力質問との類似度に基づいてLLMのためにいくつかのチャンクを取得することに焦点を当てているが、チャンクサイズとチャンク数の設定は難しく、LLMが質問に答えるための完全なコンテキストを提供しない場合、結果に影響を与える。
- [[Proposition indexing]] (@tomchen0 et al) は、検索に最適化されたドキュメントの要約 ("propositions") を生成するためにLLMを使用する手法であり、有用なアイデアである。
- この論文をベースに、2つのretrieverを構築した:
    - (1) multi-vector retrieverは要約をエンベッディングするが、LLMには完全なドキュメントを返す。
    - (2) parent-doc retrieverはチャンクをエンベッディングするが、LLMには完全なドキュメントも返す。
- 検索に適した簡潔な表現（要約またはチャンク）を使用しながら、生成には完全なコンテキストを持つドキュメントにリンクさせることで、両方の利点を得ることができる。
- このアプローチは一般的であり、テーブルや画像にも適用できる: 要約を作成・インデックス化し、LLM生成には生のテーブルや画像を返す。
- これにより、テーブル（チャンクサイズの設定が不適切だと分割されてしまう）や画像（マルチモーダルエンベッディングが必要）を直接エンベッディングする際の課題を回避し、テキストベースの類似性検索のための表現として要約を使用することができる。

> [LangChainAI](https://twitter.com/LangChainAI/status/1773387841550323929/photo/1) RAG From Scratch: Multi-Representation Indexing
>
>  Our RAG From Scratch video series walks through impt RAG concepts in short / focused videos w/ code.
>
>  This is the 12th video in our series and focuses on some useful tricks for indexing full documents.
>
>   Problem: Many RAG approaches focus on splitting documents into chunks and retrieving some number based on similarity to an input question for the LLM. But chunk size and chunk number can be difficult to set and affect results if they do not provide full context for the LLM to answer a question.
>
>  Idea: Proposition indexing (
>  @tomchen0
>   et al) is a nice paper that uses an LLM to produce document summaries ("propositions") that are optimized for retrieval. We've built on this with two retrievers.
>
>  (1) multi-vector retriever embeds summaries, but returns full documents to the LLM. (2) parent-doc retriever embeds chunks but also returns full documents to the LLM. The idea is to get best of both worlds: use concise representations (summaries or chunks) that are well-suited to retrieval, but link them to documents, which have full context for generation.
>
>  The approach is general, and can also be applied to tables or images: create / index a summary, but return the raw table or raw image for LLM generation. This gets around challenges w/ directly embedding tables (they can be split by poorly tuned chunk size) or images (need multi-modal embeddings), using a summary as a representation for text-based similarity search.
>
>   Video:
>  [https://youtu.be/gTCU9I6QqCE](https://youtu.be/gTCU9I6QqCE)
>
>   Code:
>  [https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_12_to_14.ipynb…](https://github.com/langchain-ai/rag-from-scratch/blob/main/rag_from_scratch_12_to_14.ipynb…)
>
>   References:
>  1/ Proposition indexing:  [https://arxiv.org/pdf/2312.06648.pdf…](https://arxiv.org/pdf/2312.06648.pdf…)
>  2/ Multi-vector:
>  [https://python.langchain.com/docs/modules/data_connection/retrievers/multi_vector…](https://python.langchain.com/docs/modules/data_connection/retrievers/multi_vector…)
>  3/ Parent-document:
>  [https://python.langchain.com/docs/modules/data_connection/retrievers/parent_document_retriever…](https://python.langchain.com/docs/modules/data_connection/retrievers/parent_document_retriever…)
>  4/ Blog applying this to tables:
>  [https://blog.langchain.dev/semi-structured-multi-modal-rag/…](https://blog.langchain.dev/semi-structured-multi-modal-rag/…)
>  5/ Blog applying this to images w/ eval:
>  [https://blog.langchain.dev/multi-modal-rag-template/…](https://blog.langchain.dev/multi-modal-rag-template/…)
>  ![image](https://pbs.twimg.com/media/GJxR6lWbIAA1ITr?format=jpg&name=900x900#.png)
