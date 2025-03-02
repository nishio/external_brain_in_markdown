
> On-the-fly retrieval of relevant knowledge has proven an essential element of reliable systems for tasks such as open-domain question answering and fact verification. However, because retrieval systems are not perfect, generation models are required to generate outputs given partially or entirely irrelevant passages. This can cause over- or under-reliance on context, and result in problems in the generated output such as hallucinations. To alleviate these problems, we propose FILCO, a method that improves the quality of the context provided to the generator by (1) identifying useful context based on lexical and information-theoretic approaches, and (2) training context filtering models that can filter retrieved contexts at test time. We experiment on six knowledge-intensive tasks with FLAN-T5 and LLaMa2, and demonstrate that our method outperforms existing approaches on extractive question answering (QA), complex multi-hop and long-form QA, fact verification, and dialog generation tasks. FILCO effectively improves the quality of context, whether or not it supports the canonical output.
[https://arxiv.org/abs/2311.08377](https://arxiv.org/abs/2311.08377)
(DeepL)
- 関連知識をその場で検索することは、オープンドメインの質問応答や事実検証などのタスクにおいて、信頼性の高いシステムの不可欠な要素であることが証明されている。しかし、検索システムは完全ではないため、生成モデルは、部分的または完全に無関係な文章から出力を生成する必要がある。これは、文脈への過度の依存や過小依存を引き起こし、生成された出力に幻覚のような問題をもたらす可能性がある。これらの問題を軽減するために、我々はFILCOを提案する。FILCOは、(1)語彙的・情報理論的アプローチに基づいて有用な文脈を識別し、(2)テスト時に検索された文脈をフィルタリングできる文脈フィルタリングモデルを学習することで、生成器に提供される文脈の質を向上させる手法である。FLAN-T5とLLaMa2を用いて6つの知識集約的タスクについて実験を行い、抽出的質問応答（QA）、複雑なマルチホップ・長文QA、事実検証、対話生成タスクにおいて、我々の手法が既存のアプローチを凌駕することを実証する。FILCOは、正規出力をサポートするか否かに関わらず、コンテキストの質を効果的に向上させる。

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>この論文は、知識集約型タスクにおける生成モデル向けの文脈フィルタリング手法、FILCOについて述べています。以下に要点をまとめます。

- 論文の内容: 論文は、オープンドメインの質問応答や事実検証などのタスクで重要な、関連知識のリアルタイム検索に焦点を当てています。現在の生成モデルは不完全な検索システムから部分的または全く関係のない文書を受け取ることがあり、これが生成された出力に問題を引き起こすことがあります（例えば、誤った情報の生成）。FILCOは、文脈をフィルタリングし、生成プロセスの質を向上させることを目的としています【19†source】。

- 先行研究との比較: 以前の研究では、検索された情報を生成入力として無差別に使用するのが一般的でしたが、この方法ではしばしば不関連または誤解を招く内容が含まれていました。FILCOは、文脈の品質を向上させるために、検索された情報の精細な文単位でのフィルタリングを行います【20†source】【21†source】。

- 核心技術・手法: FILCOは、検索された文脈をフィルタリングするために、(i) 文中に生成出力が含まれるかどうか（STRINC）、(ii) コンテンツと出力のユニグラム重複（LEXICAL）、(iii) コンテンツが与えられた場合の生成出力の確率（条件付き相互情報量、CXMI）を基にした手法です【21†source】。
    - > In this paper, we propose FILCO (§2), a method that learns to FILter COntext retrieved in a fine- grained sentence-wise manner, by training on con- tent selected via three measures: (i) STRINC: whether passages contain the generation output, (ii) LEXICAL overlap: how much unigram overlap the content and output has, and (iii) Conditional cross-mutual information (CXMI): how much more likely the generator is to generate the output when the content is provided.

- 方法の検証: この手法は、FLAN-T5とLLAMA2モデルを用いて、抽出型QA、複雑なマルチホップQA、長文QA、事実検証、対話生成などの6つの知識集約型タスクで検証されました。結果として、FILCOはこれらのタスクにおいて基本的なアプローチよりも優れたパフォーマンスを示しました【24†source】【25†source】【27†source】。

- 議論・批判: 研究者はFILCOを他のフィルタリング戦略と比較し、異なるタスクで最も適切なフィルタリング方法を議論しました。例えば、抽出型タスクではSTRINCが、対話生成ではLEXICALが、より複雑なタスクではCXMIが最も効果的であることが示されました【30†source】【31†source】。
    - ![image](https://gyazo.com/d20072972ba80021a2690ed27e18ad89/thumb/1000)

- 推奨されるフォローアップ読書: 関連研究では、検索結果の後処理や生成に関する最適化、異なる粒度での情報の検索などが探求されています。FILCOと関連する先行研究には、Lewis et al. (2020), Guu et al. (2020), Mi alon et al. (2023), Wang et al. (2019), Asai et al. (2022) などが含まれます【32†source】。

この論文は、知識集約型タスクにおける生成モデルの文脈品質を改善する新しいアプローチを提案しており、その効果を実証しています。また、異なるタスクのための適切な文脈フィルタリング戦略を示唆しています。






