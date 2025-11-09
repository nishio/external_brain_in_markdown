---
title: "Graph Retrieval-Augmented Generation: A Survey"
---

from [[GraphRAG]]
[[Graph Retrieval-Augmented Generation: A Survey]]
[https://arxiv.org/abs/2408.08921](https://arxiv.org/abs/2408.08921)
![image](https://gyazo.com/5ab30b83b00a9bd520b88793b9dbe9ce/thumb/1000)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
RAGの弱点（関係性を無視、冗長コンテキスト、全体像の欠落）を、グラフ構造（KG/TAG）の活用で補い、より正確・文脈理解の深い生成を実現するための技術体系を整理した総説。

何が新しいか
- GraphRAGの定式化：
    1. [[G-Indexing]]（グラフ構築・索引化）
    2. [[G-Retrieval]]（ノード/トリプル/パス/サブグラフの取得）
    3. [[G-Generation]]（取得グラフを入力に生成）
- 文字列RAGでは拾いにくい関係知識・グローバル構造を活用し、QFSなどでも有利。

G-Indexing（グラフ基盤）
- データ源：オープンKG（Wikidata/ConceptNet等）／自前構築（文書・表・ログからのTAG化）。
    - TAGとは
        - [[Text-Attributed Graphs]]
        - ![image](https://gyazo.com/c396d5e90954dd9ff2c2ac88c6abae18/thumb/1000)
        - NGは[[Knowledge Graph]]のこと
            - 従来Knowledge Graphと呼ばれていたものから一段階抽象化したということ
- 索引：
    - グラフ索引（構造探索）
    - テキスト索引（テンプレ変換→BM25/密検索）
    - ベクトル索引（ノード/エゴネット埋め込み）
    - ハイブリッド推奨。

G-Retrieval（取得）
- リトリーバ：非パラメトリック（BFS/最短路/PCST）、LM系、GNN系、または複合。
- パラダイム：一括／反復（適応/非適応）／多段（粗→精）。
- 粒度：ノード・トリプル・パス・サブグラフ・混在。
- 強化：クエリ拡張/分解、知識のマージ/剪定（再ランキング、PageRank、LLMチェック等）。

G-Generation（生成）
- 生成器：
    - GNN（判別タスクに強い）
    - LM（生成/推論に強い）
    - ハイブリッド：カスケード（GNN→LM前置き）／並列（表現結合・出力統合）。
- グラフのLM入力形式：
    - グラフ言語（エッジ表、自然文、コード風表記、構文木、ノード列）
    - グラフ埋め込み（Prefix/Prompt TuningやFiDで融合）。
- 生成強化：事前（書き換え・計画）／途中（制約デコード等）／事後（回答統合・検証）。

学習
- 学習不要：規則探索＋プロンプト、埋め込み類似。
- 学習あり：監督/遠隔監督/RL/自己教師でリトリーバ・生成器を最適化。
- 共同学習：交互学習や統合目的で相互強化。

適用・評価
- タスク：KBQA/CSQA、EL/RE、ファクト検証、リンク予測、対話、推薦。
- 領域：Eコマース、医療、学術、法務、文芸など。
- ベンチ：WebQSP/CWQ/HotpotQA等、STaRK・GraphQA・GRBENCH・CRAG。
- 指標：EM/F1/Accuracy/BLEU類＋取得品質（被覆・多様性・忠実度）。

産業事例
- Microsoft GraphRAG（コミュニティ要約でQFS強化）、NebulaGraph版、Ant Group版、Neo4j NaLLM/Graph Builder など。

今後の論点
- 動的グラフ更新と適応、マルチモーダル統合、大規模グラフでの効率化、
- Graph Foundation Modelsとの連携、ロスレス圧縮で長文脈問題緩和、標準ベンチ整備、応用拡張。

実務のヒント（超要約）
- 小規模でもハイブリッド索引＋多段取得で精度/コスト最適化。
- タスクに合わせて粒度（パス/サブグラフ中心）を選択。
- LM入力は短く・完全・可読なグラフ言語に（必要ならコミュニティ要約）。
- 重要局面は再ランキング/剪定と事後検証を入れると安定します。

