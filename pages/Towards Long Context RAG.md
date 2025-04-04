---
title: "Towards Long Context RAG"
---

[Towards Long Context RAG — LlamaIndex, Data Framework for LLM Applications](https://www.llamaindex.ai/blog/towards-long-context-rag)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
LlamaIndexは、GoogleのGemini 1.5 Proなどの大文脈LLMの登場により、RAGアーキテクチャがどのように進化するかについての考えを述べています。
大文脈LLMにより、チャンク化アルゴリズムの調整や、単一文書に対する検索と思考の連鎖の調整などの問題点が解決されますが、大規模文書コーパスに対する検索、埋め込みモデルの文脈長、コストと待ち時間などの課題は残ります。
これらの課題に対処しつつ大文脈LLMの能力を活用するために、新しいRAGアーキテクチャが必要になります。LlamaIndexが提案するのは以下の3つです。
- 小さなチャンクから大きなチャンクへの検索
- 待ち時間とコストのトレードオフのためのインテリジェントなルーティング
- 検索による補完を加えたKVキャッシュ

# 大文脈LLMの課題
1. 大規模文書コーパスに対する検索の限界
        - - 1Mトークンは約7つのUber SEC 10Kファイリングに相当
        - - 10Mトークンは約70のファイリングに相当し、約40MBのデータに制限される
        - - 多くの企業の知識コーパスはギガバイトまたはテラバイト単位であり、これらの知識コーパスに対してLLMを活用するシステムを構築するには、まだデータを取得する方法を構築する必要がある

2. 埋め込みモデルの文脈長の遅れ
        - - 現在、最大の文脈窓は、together.aiの32kトークン
        - - 大文脈LLMで合成に使用されるチャンクは大きくできるが、検索に使用されるテキストチャンクはまだかなり小さくする必要がある

3. コストと待ち時間の問題
        - - 1Mの文脈窓に情報を詰め込むのに約60秒かかり、現在の価格では0.50ドルから20ドルの費用がかかる可能性がある
        - - KVキャッシュを使用してドキュメントのアクティベーションをキャッシュし、後続の生成で同じキャッシュを再利用することで、この問題は緩和される可能性がある

4. KVキャッシュの課題
        - - 1Mトークン分のアクティベーションをキャッシュするには、約100GBのGPUメモリ、つまり2つのH100が必要
        - - 基盤となるコーパスが大きい場合、キャッシュを最適に管理する方法にも課題がある
        - - 各アクティベーションはそれまでのすべてのトークンの関数であるため、KVキャッシュ内のドキュメントを置き換えると、そのドキュメントに続くすべてのアクティベーションに影響を与える

以上が、大文脈LLMの主な課題です。これらの課題に対処しつつ、大文脈LLMの能力を最大限に活用するためには、新しいRAGアーキテクチャの開発が必要不可欠だと考えられます。

# LlamaIndexが提案する新しいRAGアーキテクチャ

1. 小さなチャンクから大きなチャンクへの検索
        - - 大文脈LLMが大規模な知識ベース（ギガバイト単位）に対して検索による補完を必要とする場合、小さなチャンクからインデックスを作成・検索し、各チャンクを最終的に合成の際にLLMに入力される大きなチャンクにリンクさせる必要がある
        - - この方法は、文書の要約をインデックス化し、文書全体にリンクさせる方法と、文書内の小さなチャンクをインデックス化し、文書にリンクさせる方法の2つの形で実現できる
        - - 小さなチャンクを埋め込んでインデックス化する理由は、現在の埋め込みモデルの文脈長がLLMに追いついていないことと、文書全体の埋め込みよりも細かい複数の埋め込み表現の方が関連情報の検索に有利な場合があるため

2. 待ち時間とコストのトレードオフのためのインテリジェントなルーティング
        - - 各ユースケースに適した文脈量は、コストと待ち時間のトレードオフを考慮して慎重に検討する必要がある
        - - 具体的な詳細を尋ねる質問には、既存のRAG手法（トップk検索と合成）が適している
        - - 要約や複数の文書にまたがる複雑な質問には、より多くの文脈が必要となる
        - - 質問に応じて、コストと待ち時間の面で最適な戦略を選択できるインテリジェントなルーティング層を、複数のRAGとLLM合成パイプラインの上に配置することを想定

3. 検索による補完を加えたKVキャッシュ
        - - KVキャッシュを使用して文脈ウィンドウ内のすべてのドキュメントトークンをキャッシュすることで、後続の会話でこれらのトークンのアクティベーションを再計算する必要がなくなり、待ち時間とコストを大幅に削減できる
        - - 文脈長を超える知識コーパスに対しては、ユーザーが回答に使いたいと思う最も関連性の高い文書を取得する「検索によるキャッシング」のパラダイムが登場すると想定
        - - これには、LRUキャッシュなどの従来のキャッシュアルゴリズムと検索戦略を交互に行うことが含まれる
        - - 位置が重要であり、キャッシュされたベクトルはドキュメント自体のトークンだけでなく、その位置までのすべてのトークンの関数であるため、KVキャッシュからチャンクを入れ替えると、その後に位置的に発生するすべてのキャッシュされたトークンに影響を与える点が従来のKVキャッシュアーキテクチャとは異なる

以上が、LlamaIndexが提案する新しいRAGアーキテクチャの詳細です。これらのアーキテクチャを通じて、大文脈LLMの課題に対処しつつ、その能力を最大限に活用することが期待されます。

[[Long Context]]
[[RAG]]
