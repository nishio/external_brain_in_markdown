---
title: "GraphRAG関連サーベイ"
---

2025-09-04

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
1) なにを抽出するか（抽出ターゲットの類型）
A. 基本三点セット
- エンティティ / 関係 / 事象（イベント）：文書内・文書間での固有表現、関係リンク、出来事＋役割。
    - 代表的な抽出器として [[DyGIE++]]、[[OneIE]]、[[OpenIE]] 系（OpenIE5/6）、[[生成型 Relation Extraction]] の [[REBEL]] など。
    - これらは[[知識グラフ]]の骨格づくりに使う。
    - ([arXiv](https://arxiv.org/pdf/1909.03546?utm_source=chatgpt.com), [ACL Anthology](https://aclanthology.org/2020.acl-main.713.pdf?utm_source=chatgpt.com))
B. 時間・因果・時系列
- 時間関係（before/after/simultaneous）やイベント因果の抽出。
- 文書横断のタイムラインや因果グラフの構築に使う。
- 医療など長文・長期履歴で有効。 ([arXiv](https://arxiv.org/abs/2104.09570?utm_source=chatgpt.com), [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0950705124000455?utm_source=chatgpt.com), [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11105141/?utm_source=chatgpt.com), [ACL Anthology](https://aclanthology.org/2024.findings-emnlp.986.pdf?utm_source=chatgpt.com))
C. 論証・主張・根拠（プロヴナンス）
- 主張/反論/根拠のグラフ（[[Argument Interchange Format]]: AIF）や、出典・生成過程の[[W3C PROV]]を付与。
- 回答の説明責任や検証、再現に効く。
- ([Wikipedia](https://en.wikipedia.org/wiki/Argument_Interchange_Format?utm_source=chatgpt.com), [Centre for Argument Technology](https://www.arg-tech.org/wp-content/uploads/2011/09/aif-spec.pdf?utm_source=chatgpt.com), [W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com))
D. コア参照・正規化
- エンティティの同一性解決（別名/略称/表記揺れ）とリンク（例：Wikidata）。
- 知識グラフの一貫性・検索再現率に直結（実装上の必須前処理）。

2) どう使うか（グラフ/DAGを使う処理パターン）
① 検索・RAG（グラフ誘導型）
- [[GraphRAG]]：文書群からKG([[Knowledge Graph]])を作り、コミュニティ検出→[[階層サマリ]]を前計算。
    - ローカル検索（周辺サブグラフ＋原文チャンク）と、グローバル検索（コミュニティ・レポート横断）や[[DRIFT]]（両者の併用）で質問に応答。「全体像」系の質問に強い。 ([Microsoft GitHub](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com), [Microsoft](https://www.microsoft.com/en-us/research/blog/graphrag-new-tool-for-complex-data-discovery-now-on-github/?utm_source=chatgpt.com))
- [[HippoRAG]]：KG 上でPersonalized PageRankを使って関連ノードを広げる単段取得でも多段推論級の精度を狙う（[[HotpotQA]] 等で最大20%向上を報告）。多跳問答や探索の効率改善に寄与。 ([arXiv](https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com))
- [[LightRAG]] / [[LlamaIndex-KG]]：軽量に三つ組抽出→サブグラフRAGを回す実装系。
    - 自前グラフの統合や“低コストでグラフ併用”に向く。
    - ([lightrag.github.io](https://lightrag.github.io/?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2410.05779?utm_source=chatgpt.com), [LlamaIndex](https://docs.llamaindex.ai/en/stable/api_reference/indices/knowledge_graph/?utm_source=chatgpt.com))
- [[G-Retriever]] / [[GRAG]]：グラフQAに特化し、GNN＋LLM＋RAGで巨大グラフQAを高速・高精度化。
    - 研究目的のGraphQAやKBQAに。 ([NeurIPS Proceedings](https://proceedings.neurips.cc/paper_files/paper/2024/file/efaf1c9726648c8ba363a5c927440529-Paper-Conference.pdf?utm_source=chatgpt.com), [ACL Anthology](https://aclanthology.org/2025.findings-naacl.232.pdf?utm_source=chatgpt.com))
- サーベイ：GraphRAG の標準ワークフロー（G-Indexing→G-Retrieval→G-Generation）の俯瞰。導入前に一読推奨。 ([arXiv](https://arxiv.org/abs/2408.08921?utm_source=chatgpt.com))
② 要約・全体把握
- [[GraphRAG]]（QFS志向）：クエリ焦点型要約を、KG＋コミュニティ要約の組合せでスケールさせる。
    - 全社横断レポートや巨大コーパスのテーマ抽出に。 ([arXiv](https://arxiv.org/abs/2404.16130?utm_source=chatgpt.com))
- [[RAPTOR]]：クラスタ→[[階層サマリ木]]（Tree）を構築して検索時に適切なレベルから引く。
    - DAG/ツリー系の階層要約インデックス。 ([arXiv](https://arxiv.org/abs/2401.18059?utm_source=chatgpt.com))
③ エージェント/対話メモリ
- [[Theanine(記憶システム)]]：メモリの削除を前提にしない。過去の出来事を時間・因果リンクでタイムライン化し、**“出来事の推移/因果”**を文脈として応答生成に注入。評価枠組み TeaFarm も提示（NAACL 2025）。長期対話の文脈保持に特化。 ([arXiv](https://arxiv.org/abs/2406.10996))
- [[MemGPT]] / [[LongMem]]：メモリ階層や仮想コンテキスト管理で長履歴を扱う方向（グラフというよりメモリOS/バンク）。Theanine の時間・因果グラフとは補完関係。 ([arXiv](https://arxiv.org/abs/2310.08560?utm_source=chatgpt.com), [NeurIPS Proceedings](https://proceedings.neurips.cc/paper_files/paper/2023/file/ebd82705f44793b6f9ade5a669d0f0bf-Paper-Conference.pdf?utm_source=chatgpt.com))
④ 検証・説明・整合性チェック
- PROVで由来（誰が/何から/いつ生成）のエッジを保持し、回答時に根拠パスを提示。AIFで主張-根拠-反論の論証グラフを保持して“なぜそう言えるか”を語れる。 ([W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com), [Wikipedia](https://en.wikipedia.org/wiki/Argument_Interchange_Format?utm_source=chatgpt.com))

3) 代表アプローチの比較（要点だけ）
_
| 系統 | 主要抽出 | 使う構造 | 強み/用途（要点） |
| -- | -- | -- | -- |
| GraphRAG（Microsoft） | LLMでKG抽出＋コミュニティ検出→階層サマリ | KG＋階層（グローバル/ローカル/DRIFT） | 全体像・多文書のQFSに強い。運用手引き・実装が充実。 ([Microsoft GitHub https://microsoft.github.io/graphrag/?utm_source=chatgpt.com], [Microsoft https://www.microsoft.com/en-us/research/blog/graphrag-new-tool-for-complex-data-discovery-now-on-github/?utm_source=chatgpt.com]) |
| HippoRAG | エンティティ/関係 | KG＋Personalized PageRank | 多跳QAで低コスト高精度。単段取得でも強い。 ([arXiv https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com]) |
| LightRAG　三つ組抽出 | 軽量KG＋K/V索引 | セットアップ容易、低レイテンシ。 ([lightrag.github.io https://lightrag.github.io/?utm_source=chatgpt.com], [arXiv https://arxiv.org/abs/2410.05779?utm_source=chatgpt.com]) |
| LlamaIndex-KG | 三つ組抽出 | Subgraph RAG | 既存RAGにKGリトリーバを足す構成が簡単。 ([LlamaIndex https://docs.llamaindex.ai/en/stable/api_reference/indices/knowledge_graph/?utm_source=chatgpt.com]) |
| Theanine | 対話メモリ断片 | 時間・因果で連結したタイムライン | 長期対話で“変化の経緯”を理解して応答に反映。 ([arXiv https://arxiv.org/abs/2406.10996]) |
| RAPTOR | 埋め込み→クラスタ | 階層サマリ木（Tree/DAG） | 巨大コーパスを上位概念から段階的に検索。 ([arXiv https://arxiv.org/abs/2401.18059?utm_source=chatgpt.com]) |
| G-Retriever/GRAG | グラフQA前提 | GNN＋LLM＋RAG | 巨大グラフQAの高速/高精度化。 ([NeurIPS Proceedings https://proceedings.neurips.cc/paper_files/paper/2024/file/efaf1c9726648c8ba363a5c927440529-Paper-Conference.pdf?utm_source=chatgpt.com], [ACL Anthology https://aclanthology.org/2025.findings-naacl.232.pdf?utm_source=chatgpt.com] |





4) 実装の勘所（設計パターン）
(a) データモデル設計
- Property Graph or RDF：クエリ容易さ（Cypher）か標準語彙/相互運用性（RDF/OWL, PROV-O）か。出典/生成過程は最初から PROV で付けると後が楽。 ([W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com))
- ノード型の設計：`Entity / Event / Claim / Source / Community / Memory` 等。時間（発生/観測/有効期間）と因果は一次クラス市民。
- IDと同定：コア参照統合（同一人物/組織の別表記）。知識整備のコストを最初期に払うと、後段の多跳検索が安定する。
(b) 抽出パイプライン（最小構成）
1. 分割（段落/文/発話）→言語前処理（NER, co-ref）
2. 関係・イベント抽出：REBEL/OneIE/DyGIE++ など or LLM誘導の三つ組抽出（コスト⇆精度のトレードオフ）。 ([ACL Anthology](https://aclanthology.org/2021.findings-emnlp.204.pdf?utm_source=chatgpt.com), [arXiv](https://arxiv.org/pdf/1909.03546?utm_source=chatgpt.com))
3. 時間・因果リンク：イベント時刻/順序/因果を抽出（ルール＋LLM、あるいは既存手法）。 ([arXiv](https://arxiv.org/abs/2104.09570?utm_source=chatgpt.com))
4. 正規化/同定（KBリンク, 辞書, Embedding）
5. 格納（Graph DB / RDF ストア）＋二重インデックス（ベクトル＆グラフ）
6. （任意）階層化：GraphRAGのコミュニティ検出→レポート生成、RAPTOR の階層要約木を事前計算。 ([Microsoft](https://www.microsoft.com/en-us/research/blog/graphrag-new-tool-for-complex-data-discovery-now-on-github/?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2401.18059?utm_source=chatgpt.com))
(c) 取得（Retrieval）の作法
- ローカル：質問から種ノードを作り近傍展開＋原文チャンクを併用（GraphRAG: Local）。 ([Microsoft GitHub](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com))
- グローバル：コミュニティ要約を横断して合成（GraphRAG: Global/DRIFT）。テーマ系の質問に効く。 ([Microsoft](https://www.microsoft.com/en-us/research/blog/graphrag-improving-global-search-via-dynamic-community-selection/?utm_source=chatgpt.com))
- ランキング：PPR/短経路/中心性と埋め込みの類似度をハイブリッドに。HippoRAG は PPR が要（実装上の良い出発点）。 ([arXiv](https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com))
(d) 生成（Generation）
- プロンプトに“構造”を渡す：サブグラフ（ノード/エッジ/プロヴナンス）＋必要最小の原文テキスト。
- 階層要約の合成：GraphRAG のコミュニティ・レポート→部分回答→最終要約という段階合成は大規模でも破綻しにくい。 ([arXiv](https://arxiv.org/abs/2404.16130?utm_source=chatgpt.com))
(e) メモリ（対話/エージェント）
- Theanine流：メモリを削除せず、時間・因果で連結したタイムラインから必要部分を提示。ユーザ状態の変化・経緯理解に有効。MemGPT/LongMem は溢れた履歴の入出庫（階層メモリ）で補完。 ([arXiv](https://arxiv.org/abs/2406.10996), [NeurIPS Proceedings](https://proceedings.neurips.cc/paper_files/paper/2023/file/ebd82705f44793b6f9ade5a669d0f0bf-Paper-Conference.pdf?utm_source=chatgpt.com))
(f) 評価
- QA/要約：正確性（EM/F1）、包括性/多様性（GraphRAG 論文のQFS設定など）。 ([arXiv](https://arxiv.org/abs/2404.16130?utm_source=chatgpt.com))
- メモリ統合理解：Theanine の TeaFarm のような反事実テストで「過去の出来事の推移」を本当に使えているかを見る。 ([arXiv](https://arxiv.org/abs/2406.10996))
(g) リスクと対策
- 抽出の幻覚：LLM抽出は誤リンク/過抽象化が出る。二段階抽出（候補→検証）や出典必須で緩和。
- 更新とドリフト：新規文書のインクリ更新と、古い要約/コミュニティの再計算戦略を設計。GraphRAG はグローバル/ローカル/DRIFT の切替でコスト/品質を調整。 ([Microsoft](https://www.microsoft.com/en-us/research/blog/introducing-drift-search-combining-global-and-local-search-methods-to-improve-quality-and-efficiency/?utm_source=chatgpt.com))

5) まずの実装テンプレ（最小構成）
1. ベース：ベクトルRAG（埋め込み＋原文保存）。
2. KG 併用：LlamaIndex KnowledgeGraphIndexで三つ組を生成・格納（Neo4j でも RDF でも可）。同時に PROV-O で出典を結線。 ([LlamaIndex](https://docs.llamaindex.ai/en/stable/api_reference/indices/knowledge_graph/?utm_source=chatgpt.com), [W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com))
3. グラフ活用：
    - 近傍サブグラフ＋原文でローカルGraphRAG。 ([Microsoft GitHub](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com))
    - 必要に応じてコミュニティ検出→階層サマリを前計算（グローバルやDRIFT質問に対応）。 ([Microsoft](https://www.microsoft.com/en-us/research/blog/graphrag-new-tool-for-complex-data-discovery-now-on-github/?utm_source=chatgpt.com))
    - 多跳が多いなら HippoRAG の PPR を導入。 ([arXiv](https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com))
4. 対話メモリ：ユーザ毎に出来事ノード（発話/行動/好み）を時刻・因果で連結してタイムラインを維持（Theanineの方針）。 ([arXiv](https://arxiv.org/abs/2406.10996))

6) 使い分けの指針（ざっくり）
- **「全体像・テーマ」**を尋ねる：GraphRAG（グローバル/DRIFT） or RAPTOR。 ([arXiv](https://arxiv.org/abs/2404.16130?utm_source=chatgpt.com))
- 「手がかり少なめの多跳QA」：HippoRAG（PPR）→必要なら G-Retriever/GRAG。 ([arXiv](https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com), [NeurIPS Proceedings](https://proceedings.neurips.cc/paper_files/paper/2024/file/efaf1c9726648c8ba363a5c927440529-Paper-Conference.pdf?utm_source=chatgpt.com), [ACL Anthology](https://aclanthology.org/2025.findings-naacl.232.pdf?utm_source=chatgpt.com))
- 「低運用コストでKGを足したい」：LightRAG or LlamaIndex-KG。 ([lightrag.github.io](https://lightrag.github.io/?utm_source=chatgpt.com), [LlamaIndex](https://docs.llamaindex.ai/en/stable/api_reference/indices/knowledge_graph/?utm_source=chatgpt.com))
- 「長期対話のコンテキストを失わずに使いたい」：Theanineの時間・因果タイムライン＋必要に応じて MemGPT/LongMem。 ([arXiv](https://arxiv.org/abs/2406.10996), [NeurIPS Proceedings](https://proceedings.neurips.cc/paper_files/paper/2023/file/ebd82705f44793b6f9ade5a669d0f0bf-Paper-Conference.pdf?utm_source=chatgpt.com))

7) 補足：Graph-of-Thoughts系（“思考”のグラフ化）
抽出対象は「外部テキスト」ではなくLLMの中間思考だが、グラフ構造（再利用・分岐・合流）で推論を強化する系。外部KGと併用して推論の骨格に使える。 ([arXiv](https://arxiv.org/abs/2308.09687?utm_source=chatgpt.com))

参考・出発点リンク（抜粋）
- GraphRAG（仕組み・実装・運用ブログ） ([Microsoft GitHub](https://microsoft.github.io/graphrag/?utm_source=chatgpt.com), [Microsoft](https://www.microsoft.com/en-us/research/blog/graphrag-new-tool-for-complex-data-discovery-now-on-github/?utm_source=chatgpt.com))
- HippoRAG（NeurIPS'24） ([arXiv](https://arxiv.org/abs/2405.14831?utm_source=chatgpt.com))
- LightRAG ([lightrag.github.io](https://lightrag.github.io/?utm_source=chatgpt.com), [arXiv](https://arxiv.org/abs/2410.05779?utm_source=chatgpt.com))
- LlamaIndex: KnowledgeGraphIndex ([LlamaIndex](https://docs.llamaindex.ai/en/stable/api_reference/indices/knowledge_graph/?utm_source=chatgpt.com))
- Theanine（NAACL'25） ([arXiv](https://arxiv.org/abs/2406.10996))
- RAPTOR（ICLR'24） ([arXiv](https://arxiv.org/abs/2401.18059?utm_source=chatgpt.com))
- GraphRAG Survey（2024） ([arXiv](https://arxiv.org/abs/2408.08921?utm_source=chatgpt.com))

次の一手（実務向けメモ）
- PoCでは：①三つ組抽出＋Subgraph RAG（安価）→②コミュニティ要約/DRIFT（“全体像”質問対応）→③PPR（多跳強化）→④対話タイムライン（長期記憶）の順で拡張。
- メトリクス：QA（EM/F1）、包括性/多様性（QFS系）、反事実（TeaFarm）を混ぜる。 ([arXiv](https://arxiv.org/abs/2404.16130?utm_source=chatgpt.com))
- ポリシー：全出力にプロヴナンス（出典パス）を付与。将来の監査・可観測性に効く。 ([W3C](https://www.w3.org/TR/prov-overview/?utm_source=chatgpt.com))

必要なら、手元データ/要件（コーパス規模、質問パターン、遅延予算）に合わせて最小構成の設計図まで具体化します。

[https://chatgpt.com/c/68b7f215-cd4c-8323-b08e-f107d41fb58b](https://chatgpt.com/c/68b7f215-cd4c-8323-b08e-f107d41fb58b)

[https://chatgpt.com/c/68ba8b5f-17fc-8327-ba44-bf69ba51856c](https://chatgpt.com/c/68ba8b5f-17fc-8327-ba44-bf69ba51856c)
- [[A Framework for Constructing Concept Maps from E-Books Using Large Language Models: Challenges and Future Directions]]
