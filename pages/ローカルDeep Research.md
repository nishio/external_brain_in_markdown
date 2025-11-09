---
title: "ローカルDeep Research"
---

2025-08-29
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ローカルのファイルに対して[[Deep Research]]的なことをやる上で2025年8月現在最良の方法は?

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
西尾さん、結論から。

要点（2025年8月時点）
- 「Deep Research 的」= 企画立案レベルの多段推論＋出典付き要約。OpenAI版は多数ソースを読み込み、計画→収集→要約→必ず引用のレポートを返す設計です（最近はビジュアルブラウザ併用）。ローカルでも要件は同じ：高精度パース → ハイブリッド検索 → リランキング → 多段推論 → 厳密な引用。([OpenAI](https://openai.com/index/introducing-deep-research/?utm_source=chatgpt.com), [OpenAI Help Center](https://help.openai.com/en/articles/10500283-deep-research-faq?utm_source=chatgpt.com))

推奨アーキテクチャ（用途別の最良解）

A. 研究ノート／論文系に強い「厳密引用」特化
PaperQA2（PDF/テキストを跨ぐ高精度RAG、段落・ページ出典つき）＋好みのLLM/埋め込み
- ローカルPDF群を対象に、質問→証拠抽出→回答→ページ番号付き引用まで自動化。科学系だが一般文書にも有効。([GitHub](https://github.com/Future-House/paper-qa?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2409.13740?utm_source=chatgpt.com))
- 使い方は `Docs.add(path)`→`query()` の極小API。OpenAI/llama.cpp/Ollama等を選べる。([PyPI](https://pypi.org/project/paper-qa/4.4.0/?utm_source=chatgpt.com))
こんな時に：論文・計画書・議事録を確証つきで横断照会したい。

B. コーパス全体像の把握＋発見に強い「構造化探索」
[[GraphRAG]]（知識グラフ＋コミュニティ要約）＋ LlamaIndex/LangGraph（エージェント化）
- コーパスからエンティティ関係を自動抽出→グラフ化→ローカルQA。未知論点の発見や「鳥瞰図」に強い。([Microsoft](https://www.microsoft.com/en-us/research/project/graphrag/?utm_source=chatgpt.com), [microsoft.github.io](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com))
- LangGraphを併用すると、計画→収集→検証→レポートの長期タスクを状態保持しながら回せる。([langchain-ai.github.io](https://langchain-ai.github.io/langgraph/?utm_source=chatgpt.com))
こんな時に：大量資料の論点抽出・地図化、調査設計の反復。

C. GUIで手っ取り早く「自炊した知識ベースに質問」
AnythingLLM / PrivateGPT / Danswer のいずれか＋ローカルLLM
- 自前UIでPDF/MD/Docをドロップ→チャット検索。オンプレ完結構成も可能。([garmingo.com](https://garmingo.com/blog/p/self-host-anythingllm?utm_source=chatgpt.com), [GitHub](https://github.com/zylon-ai/private-gpt?utm_source=chatgpt.com), [zenml.io](https://www.zenml.io/llmops-database/scaling-enterprise-rag-with-advanced-vector-search-migration?utm_source=chatgpt.com))
こんな時に：構築コスト最小で試したい、チームに配りたい。

共通の“最良”レシピ（部品の指名買い）
1. パース（PDF/Office）
- レイアウト保持のDocling（IBM） or Marker（数式・表に強い）＋用途により Unstructured（要素ラベル付き分割）。([IBM Research](https://research.ibm.com/blog/docling-generative-AI?utm_source=chatgpt.com), [GitHub](https://github.com/datalab-to/marker?utm_source=chatgpt.com), [Unstructured](https://unstructured.io/blog/how-to-parse-a-pdf-part-1?utm_source=chatgpt.com))
2. インデクシング（ハイブリッド）
- BM25（SQLite-vec か Tantivy系）＋ 埋め込みの二段。SQLite運用なら `sqlite-vec` が軽量。([GitHub](https://github.com/asg017/sqlite-vec?utm_source=chatgpt.com))
- ベクタDBは Qdrant（堅実）か LanceDB（列指向・同一フォーマットでデータとベクトル同居）。([qdrant.tech](https://qdrant.tech/?utm_source=chatgpt.com), [https://lancedb.com/?utm_source=chatgpt.com](https://lancedb.com/))
3. 埋め込み（日本語+英語）
- 商用：Voyage-3/4系が2025年評価で強い報告。([datastax.com](https://www.datastax.com/blog/best-embedding-models-information-retrieval-2025?utm_source=chatgpt.com))
- OSS重視：Jina-embeddings-v3 は多言語MTEBで好成績。([jina.ai](https://jina.ai/news/jina-embeddings-v3-a-frontier-multilingual-embedding-model/?utm_source=chatgpt.com))
（※最終選定は自前データでRAGAS/TruLens等で評価を）([docs.ragas.io](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/faithfulness/?utm_source=chatgpt.com), [trulens.org](https://www.trulens.org/blog/archive/2025/?utm_source=chatgpt.com))
4. リランキング（品質の要）
- API可なら Voyage rerank-2.5（長文32k対応・最新ベンチ良）。完全ローカルなら bge-reranker-v2-m3（多言語）。([Voyage AI](https://blog.voyageai.com/2025/08/11/rerank-2-5/?utm_source=chatgpt.com), [Hugging Face](https://huggingface.co/BAAI/bge-reranker-v2-m3?utm_source=chatgpt.com))
5. 多段推論オーケストレーション
- LangGraphで「計画→収集→検証→要約→引用整形」をグラフ化（永続メモリ可）。([langchain-ai.github.io](https://langchain-ai.github.io/langgraph/?utm_source=chatgpt.com))
- MCP（Model Context Protocol）でローカルFSを安全にツール化し、エージェントからファイル参照。([openai.github.io](https://openai.github.io/openai-agents-python/ja/mcp/?utm_source=chatgpt.com), [The Verge](https://www.theverge.com/news/669298/microsoft-windows-ai-foundry-mcp-support?utm_source=chatgpt.com))
6. 引用・検証
- 出典必須なら PaperQA2を最終生成器に据える／あるいはCitekit系を併用。([GitHub](https://github.com/Future-House/paper-qa?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2408.04662?utm_source=chatgpt.com))
7. 長文対策（コンテキスト圧縮）
- LLMLingua-2 や Provence の文/トークン単位の剪定で迷入文脈を除去し、コストと幻覚を抑える。([Microsoft](https://www.microsoft.com/en-us/research/project/llmlingua/llmlingua-2/?utm_source=chatgpt.com), [proceedings.iclr.cc](https://proceedings.iclr.cc/paper_files/paper/2025/file/5e956fef0946dc1e39760f94b78045fe-Paper-Conference.pdf?utm_source=chatgpt.com))
8. ローカル実行基盤
- LLM実行は Ollama or LM Studio（GUI/API）。Apple Siliconなら MLX。VRAMはモデルサイズ＋αを推奨。([ollama.com](https://ollama.com/?utm_source=chatgpt.com), [LM Studio](https://lmstudio.ai/?utm_source=chatgpt.com), [GitHub](https://github.com/ml-explore/mlx-lm?utm_source=chatgpt.com), [Windows Central](https://www.windowscentral.com/artificial-intelligence/when-it-comes-to-running-ollama-on-your-pc-for-local-ai-one-thing-matters-more-than-most-heres-why?utm_source=chatgpt.com))

すぐ動く最小構成（CLI志向）
- 目的：ローカルPDF群に深掘り質問→ページ引用つき回答
- 構成：Docling → LanceDB or Qdrant → Jina v3埋め込み → bge-reranker-v2-m3 → PaperQA2
- 理由：パース精度・多言語・完全オンプレ可・引用強。([GitHub](https://github.com/docling-project/docling?utm_source=chatgpt.com), [https://lancedb.com/?utm_source=chatgpt.com](https://lancedb.com/), [jina.ai](https://jina.ai/news/jina-embeddings-v3-a-frontier-multilingual-embedding-model/?utm_source=chatgpt.com), [Hugging Face](https://huggingface.co/BAAI/bge-reranker-v2-m3?utm_source=chatgpt.com))

評価と運用
- RAGAS/TruLens/ARESで faithfulness / context relevance / answer relevance を定期計測し、埋め込み・分割・リランカをAB。([docs.ragas.io](https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/faithfulness/?utm_source=chatgpt.com), [trulens.org](https://www.trulens.org/blog/archive/2025/?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2311.09476?utm_source=chatgpt.com))
- 監査ログ：どのファイルのどのページを引用したかを常に保存（Deep Researchの「常に出典」哲学を踏襲）。([OpenAI Help Center](https://help.openai.com/en/articles/10500283-deep-research-faq?utm_source=chatgpt.com))

迷ったらこの二択
1. 厳密引用・研究型：PaperQA2（生成）＋Docling（パース）＋Jina v3（埋め込み）＋bge-reranker-v2-m3（ローカル）。([GitHub](https://github.com/Future-House/paper-qa?utm_source=chatgpt.com), [IBM Research](https://research.ibm.com/blog/docling-generative-AI?utm_source=chatgpt.com), [jina.ai](https://jina.ai/news/jina-embeddings-v3-a-frontier-multilingual-embedding-model/?utm_source=chatgpt.com), [Hugging Face](https://huggingface.co/BAAI/bge-reranker-v2-m3?utm_source=chatgpt.com))
2. 探索・発見・地図化：[[GraphRAG]]＋LlamaIndex／LangGraph＋[[Voyage rerank]]（またはbge）。([Microsoft](https://www.microsoft.com/en-us/research/project/graphrag/?utm_source=chatgpt.com), [microsoft.github.io](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com), [langchain-ai.github.io](https://langchain-ai.github.io/langgraph/?utm_source=chatgpt.com), [Voyage AI](https://blog.voyageai.com/2025/08/11/rerank-2-5/?utm_source=chatgpt.com))

