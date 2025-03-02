---
title: "Dense X Retrieval: What Retrieval Granularity Should We Use?"
---

[[RAGの粒度]]に関して、指示語などを置き換えて文脈なしに理解可能な「命題」を抽出し、命題単位の埋め込みを作るアプローチ

> Dense X Retrieval: What Retrieval Granularity Should We Use?
> Tong Chen, Hongwei Wang, Sihao Chen, Wenhao Yu, Kaixin Ma, Xinran Zhao, Hongming Zhang, Dong Yu
> Dense retrieval has become a prominent method to obtain relevant context or world knowledge in open-domain NLP tasks. When we use a learned dense retriever on a retrieval corpus at inference time, an often-overlooked design choice is the retrieval unit in which the corpus is indexed, e.g. document, passage, or sentence. We discover that the retrieval unit choice significantly impacts the performance of both retrieval and downstream tasks. Distinct from the typical approach of using passages or sentences, we introduce a novel retrieval unit, proposition, for dense retrieval. Propositions are defined as atomic expressions within text, each encapsulating a distinct factoid and presented in a concise, self-contained natural language format. We conduct an empirical comparison of different retrieval granularity. Our results reveal that proposition-based retrieval significantly outperforms traditional passage or sentence-based methods in dense retrieval. Moreover, retrieval by proposition also enhances the performance of downstream QA tasks, since the retrieved texts are more condensed with question-relevant information, reducing the need for lengthy input tokens and minimizing the inclusion of extraneous, irrelevant information.
[https://arxiv.org/abs/2312.06648](https://arxiv.org/abs/2312.06648)

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
- 文書検索において、検索単位の粒度（文書、文、命題など）が検索性能に大きな影響を与えることが明らかになった。
- 従来の文書や文単位ではなく、命題（proposition）を新しい検索単位として提案。命題とは、文章中の事実を表す最小の表現単位。
- Wikipediaを100単語の文書、文、命題の3つの粒度でインデックス化したFACTOIDWIKIを構築。
- 5つのQAデータセットで6種類の検索モデルを評価したところ、命題単位の検索が文書や文単位よりも高い性能を示した。
- 特に、検索モデルの学習データに含まれないドメインでは、命題単位の検索が大きく優れていた。
- QAタスクにおいても、同じトークン数の制限下では、命題単位の検索が最も高い精度を達成。
- 命題は圧縮された形式ながら文脈情報に富むため、質問関連の情報密度が高くなると考えられる。
- 本研究の知見とFACTOIDWIKIが、情報検索の発展に貢献することを期待。

![image](https://gyazo.com/ee2dd5043850ffe30038c6eb0f9d86e9/thumb/1000)
[[Proposition indexing]]

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>命題をどうやってインデックスする？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>命題をインデックス化する具体的な手順は以下の通りです。
- Wikipediaの各ページを段落に分割する。
- 各段落を命題に分割するために、GPT-4を用いて命題分割のためのデータセットを作成する。
    - GPT-4にプロンプトを与えて、段落を命題のリストに変換。
    - 4万対以上の段落と命題リストのペアを収集。
- 収集したデータセットを用いて、命題分割モデル（Propositionizer）を学習する。
    - Flan-T5-Largeをベースモデルに使用。
    - 段落を入力し、命題のリストを出力するようにファインチューニング。
- 学習したPropositionizerを用いて、全てのWikipediaページを命題に分割する。
    - 各段落を命題のリストに変換。
    - 最終的に2億5千万以上の命題が生成される。
- 分割された命題をインデックス化する。
- [[pyserini]]と[[faiss]]ライブラリを使用。
- 各命題をバッチ処理で埋め込みベクトルに変換。
- ベクトルをインデックス化し、効率的な近似最近傍探索を可能に。
- 検索時には、クエリを埋め込みベクトルに変換し、インデックスを検索して関連する命題を効率的に取得。

以上の手順により、Wikipediaの全ページを命題単位でインデックス化したFACTOIDWIKIを構築することができる。大規模な命題のインデックス化には、GPUの並列化や分散インデックスなども活用して、オンライン検索を高速化している。

GPT4で教師データを作ってそのデータでモデルを学習して、それをWikipedia全ページの処理に使うわけね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>"GPT-4にプロンプトを与えて、段落を命題のリストに変換" ここを詳しく

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>GPT-4を使って段落を命題のリストに変換する手順は以下の通りです。
- 命題の定義と分割方法を明確にしたプロンプトを作成する。例えば以下のようなプロンプトを使用。
    - 以下の手順で、与えられた段落を明確でシンプルな命題のリストに分割してください。
    - 複文を単文に分割する。できるだけ元の表現を維持すること。
    - 名詞句に付加情報がある場合は、それを独立した命題に分割する。
    - 代名詞を参照先の名詞に置き換えるなどして、命題を[[脱文脈化]]する。
        - なるほど〜<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - 事実は[[文脈から切り離し]]て[[アトミック]]にすることが容易だろうが、一般にそうだろうか
            - [[考える花火]]のように、元々別れているものを網目にしていく活動もある
    - 結果をJSON形式のリストで出力する。
- プロンプトの後に、命題に分割したいWikipediaの段落を入力として与える。
- GPT-4にプロンプトと入力段落を与えて、命題のリストを生成させる。
- 生成された命題リストを確認し、必要に応じて手動で修正を加える。
- 十分な質の命題リストが得られるまで、ステップ2-4を繰り返す。
- 以下は、実際のプロンプトと出力例です。

![image](https://gyazo.com/3a0ab713a473485e7afbba4beecdb5a6/thumb/1000)

この手順を4万件以上の段落に対して実行し、段落と命題リストのペアからなるデータセットを作成した。この大規模な データセットにより、[[命題分割モデル]]を効果的に学習することが可能になった。
