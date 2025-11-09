---
title: "Augmenting Textual Generation via Topology Aware Retrieval"
---

[https://arxiv.org/abs/2405.17602](https://arxiv.org/abs/2405.17602)

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>何の論文？
[[Topo-RAG]] (Topology-aware Retrieval-Augmented Generation)。引用・共購買・メール往来などでテキスト同士がグラフで結ばれている状況を前提に、語義の近さだけでなくグラフの位相的な近さでリトリーブして生成を強化する手法を提案。対象はQAではなくテキスト生成（要約・書き足し）です。([arXiv](https://arxiv.org/html/2405.17602v1))
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Cosenseのようなリンク構造のあるデータに適してそう

核心アイデア（2種類の「近さ」）
- 近接ベース（proximity）：グラフ上で少ないホップで到達できるノードを近いとみなす。実装は**拡散（diffusion）**で得た埋め込みのコサイン類似度。計算は本来重いが、ランダム射影で高速化。([arXiv](https://arxiv.org/html/2405.17602v1))
- 役割ベース（role/structure）：局所構造が似た役割を持つノード（例：同じ職位の社員）。実装はGraphWaveで得た構造埋め込みのL2距離。([arXiv](https://arxiv.org/html/2405.17602v1))
まず、テキスト類似度と位相的類似度には正の相関があることを実証（論文・レビュー・メールの複数データセットで確認）。そのうえで、位相的に近い文書をTop-K取得してプロンプトに挿入し、LLMで生成する。([arXiv](https://arxiv.org/html/2405.17602v1))

フレームワーク（Topo-RAG）
1. 全ノード対で位相的類似度を前計算（空間はTop-Kでスパース化）。
2. 生成対象ノードの冒頭語（部分観測テキスト）＋位相Top-K文書をプロンプト化。
3. LLM（論文では GPT-3/3.5）で残りのテキストを生成。([arXiv](https://arxiv.org/html/2405.17602v1))

実験設計
- 9データセット / 3ドメイン：Citation（Cora, PubMed, ArXiv）、E-commerce（Amazon Product/Book/Epinion/Music/Pantry）、Social（Enron-Email）。([arXiv](https://arxiv.org/html/2405.17602v1))
- 比較：None（追加なし）／Random／Text（意味類似で検索）／Topo（本手法）。
- 指標：BLEU-4 / ROUGE-L / BERT-F1 に加え、ノード分類/リンク予測で下流性能も評価。([arXiv](https://arxiv.org/html/2405.17602v1))

主な結果
- 平均性能（GPT-3.5）：Text比で BLEU +61.8%, ROUGE +7.6%, BERT-F1 +1.0%。
平均性能（GPT-3）：Text比で BLEU +51.3%, ROUGE +6.2%, BERT-F1 +1.2%。([arXiv](https://arxiv.org/html/2405.17602v1))
- 下流タスクでも一貫してTop-RAGが最良（例：Cora/GCN で分類 71.09→75.49%、リンク予測 77.15→89.12）。([arXiv](https://arxiv.org/html/2405.17602v1))
- 冒頭語が少ないほどTopo-RAGの利得が大きい（情報が乏しいと位相補完の効きが強い）。([arXiv](https://arxiv.org/html/2405.17602v1))

既存法との違い
知識グラフ由来のトリプル近傍を足すKG-RAGはQA中心が多いのに対し、Topo-RAGはグラフの位相パターン（近接/役割）そのものを使い、生成に効かせる点が新しい。([arXiv](https://arxiv.org/html/2405.17602v1))

実装上の注意
- 位相類似度の前計算は重い（全対全）。本論文はTop-Kスパース化＋オフライン計算で運用を想定。長文の取り回しは既存の長文対策と併用。([arXiv](https://arxiv.org/html/2405.17602v1))

どこで効く？
- 論文執筆支援（引用網）／ECレビュー生成（共購買・同一ユーザ連結）／社内メール・FAQ（部門/職位での役割類似）。意味類似だけのRAGより文体・用語の寄せに強い傾向。([arXiv](https://arxiv.org/html/2405.17602v1))

限界・留意
- グラフが無い/薄い領域では使いにくい。
- BERT-F1の伸びは小さめ（語彙・言い回しの一致に効きやすい）。
- 相関が弱いデータ（例：Epinion）では利得も相対的に小さくなり得る。([arXiv](https://arxiv.org/html/2405.17602v1))
必要なら、手元データで位相特徴（diffusion/GraphWave）→Top-K取得→プロンプト設計までの最小実装サンプルも用意できます。

