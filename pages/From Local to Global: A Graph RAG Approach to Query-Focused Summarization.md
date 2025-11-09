---
title: "From Local to Global: A Graph RAG Approach to Query-Focused Summarization"
---

[https://arxiv.org/abs/2404.16130](https://arxiv.org/abs/2404.16130)
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>[[GraphRAG]]は、コーパス全体を俯瞰する“グローバル系の質問”（例：主要テーマは？相反する視点は？）に強いRAG手法。事前にエンティティ関係グラフを作り、コミュニティ（クラスタ）ごとの要約を生成。質問時はそれらをMap→Reduce合成して最終回答を出します。([arXiv](https://arxiv.org/html/2404.16130v2))

何をした研究か
- 従来の「ベクトルRAG」は局所的事実の取り出しには強いが、全文脈の要約・総合（sensemaking）には弱い、という課題設定。そこでGraphRAGを提案。([arXiv](https://arxiv.org/html/2404.16130v2))
- パイプライン（図1）
    1. 文書→チャンク化
    2. 各チャンクからエンティティ・関係・（必要に応じて）クレームをLLMで抽出
    3. それらで知識グラフを構築
    4. [[Leiden法]]などでグラフをコミュニティ分割
    5. 各コミュニティの要約を生成（階層的にボトムアップ）
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[ボトムアップ要約生成]]
    6. 質問に対して各コミュニティ要約から部分回答（Map）→結合して全体回答（Reduce）。([arXiv](https://arxiv.org/html/2404.16130v2))
- エンティティ抽出はマルチパートのプロンプトで実施。大きめチャンクで見落としが増える問題に対し、self-reflection（自己反省）プロンプトで取りこぼしを補います。([arXiv](https://arxiv.org/html/2404.16130v2))

どう評価したか
- データセット（約100万トークン規模を想定）
    - Podcast: Behind the Tech with Kevin Scott の公開トランスクリプト（600トークンチャンク×1669、オーバーラップ100）。
    - News: 2013/9–2023/12のニュース（600トークンチャンク×3197、オーバーラップ100）。([arXiv](https://arxiv.org/html/2404.16130v2))
- 条件比較：GraphRAGの4階層（C0–C3）、テキスト直接要約（TS）、ベクトルRAG（SS）。生成プロンプトやコンテキスト窓は統一。コミュニティ検出はgraspologicでLeiden。([arXiv](https://arxiv.org/html/2404.16130v2))
- 評価指標はLLM-as-a-judgeでの相対評価（包括性・多様性・エンパワーメント・対照として直接性）。さらにClaimifyで抽出した事実主張数とクラスタ数で客観指標も併用。([arXiv](https://arxiv.org/html/2404.16130v2))

主な結果
- グローバル系手法（GraphRAG/TS）＞ベクトルRAG
    - 包括性の勝率：Podcastで72–83%、Newsで72–80%。
    - 多様性の勝率：Podcastで75–82%、Newsで62–71%。
    - 一方、直接性はベクトルRAGが最も高い（＝短く直截）。([arXiv](https://arxiv.org/html/2404.16130v2))
- 効率面：ルート層C0は、質問あたりトークン消費が9–43倍少ない（全体把握の反復探索に有利）。階層が深いほど情報量は増えるがトークンも増える。([arXiv](https://arxiv.org/html/2404.16130v2))
- 客観指標でも、グローバル系がベクトルRAGより**主張数（包括性）と主張クラスタ数（多様性）**で優位（p<.05 など）。([arXiv](https://arxiv.org/html/2404.16130v2))

実装のコツ（論文から）
- チャンクサイズ：大きすぎると抽出漏れが増えるため、self-reflection併用でバランスを取る。([arXiv](https://arxiv.org/html/2404.16130v2))
- 階層の使い分け：
    - C0（最上位コミュニティ要約）＝超低コストで反復探索。
    - C2/C3（下位）＝包括性・多様性を少し伸ばしたいとき。([arXiv](https://arxiv.org/html/2404.16130v2))
- インデクシングの現実的コスト：例としてGPT-4-turboで600トークン窓、Podcast語彙で約281分程度（VM構成やAPI条件明記）。([arXiv](https://arxiv.org/html/2404.16130v2))
- OSS：Microsoftの実装あり。LangChain/LlamaIndex/NebulaGraph/Neo4j向け拡張も。([arXiv](https://arxiv.org/html/2404.16130v2))

限界と今後
- 約100万トークン規模・2コーパスでの検証に限られる。分野横断の一般化や幻覚率の比較（SelfCheckGPT等）などは今後の課題。([arXiv](https://arxiv.org/html/2404.16130v2))

いつGraphRAGを使うと良いか（私見）
- 「全体像・論点の網羅と多視点」が問われる質問（動向整理、相反する見解の俯瞰、主要テーマ抽出）。
- 同じデータに何度もグローバル質問を投げるワークロード（C0で低コスト反復→必要に応じて下位層へ“掘る”）。
※ 個別事実の正確な特定だけが目的なら、従来のベクトルRAGの方が短く直接的な回答になりやすい。([arXiv](https://arxiv.org/html/2404.16130v2))
