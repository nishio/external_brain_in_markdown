
[[Precise Zero-Shot Dense Retrieval without Relevance Labels]]
> While dense retrieval has been shown effective and efficient across tasks and languages, it remains difficult to create effective fully zero-shot dense retrieval systems when no relevance label is available. In this paper, we recognize the difficulty of zero-shot learning and encoding relevance. Instead, we propose to pivot through Hypothetical Document Embeddings~(HyDE). Given a query, HyDE first zero-shot instructs an instruction-following language model (e.g. InstructGPT) to generate a hypothetical document. The document captures relevance patterns but is unreal and may contain false details. Then, an unsupervised contrastively learned encoder~(e.g. Contriever) encodes the document into an embedding vector. This vector identifies a neighborhood in the corpus embedding space, where similar real documents are retrieved based on vector similarity. This second step ground the generated document to the actual corpus, with the encoder's dense bottleneck filtering out the incorrect details. Our experiments show that HyDE significantly outperforms the state-of-the-art unsupervised dense retriever Contriever and shows strong performance comparable to fine-tuned retrievers, across various tasks (e.g. web search, QA, fact verification) and languages~(e.g. sw, ko, ja).
- [https://arxiv.org/abs/2212.10496](https://arxiv.org/abs/2212.10496)

(DeepL)密な検索はタスクや言語を問わず効果的かつ効率的であることが示されているが、関連性ラベルが利用できない場合、効果的な完全ゼロショット密検索システムを作成することは依然として困難である。本稿では、ゼロショットの学習と関連性の符号化の難しさを認識する。その代わりに、我々は[[仮説的文書埋め込み]]（[[Hypothetical Document Embeddings]]:[[HyDE]]）によるピボット化を提案する。クエリが与えられると、HyDEはまずゼロショットで命令追従型言語モデル（例えば[[InstructGPT]]）に仮想文書を生成するよう指示する。この文書は関連性パターンを捉えるが、非現実的であり、誤った詳細を含む可能性がある。次に、教師なし対照学習されたエンコーダ～（[[Contriever]]など）が文書を[[埋め込みベクトル]]にエンコードする。このベクトルはコーパスの埋め込み空間における近傍を特定し、ベクトルの類似性に基づいて類似した実際の文書を検索する。この第二のステップは、エンコーダの高密度なボトルネックが不正確な詳細をフィルタリングすることで、生成された文書を実際のコーパスに接地する。我々の実験によれば、HyDEは最新の教師なし密文検索であるContrieverを大幅に上回り、様々なタスク（ウェブ検索、QA、事実検証など）と言語（sw、ko、jaなど）において、微調整された検索に匹敵する強力な性能を示す。

> この第二のステップは、エンコーダの高密度なボトルネックが不正確な詳細をフィルタリングすることで、生成された文書を実際のコーパスに接地する。
- ここが面白いところで、ステップ1で運悪くハルシネーションが起きてしまっても、それをベクトルに埋め込む段階で低確率な詳細はドロップされるから検索に支障ないと主張している


> ユーザーのクエリをエンコードして関連ドキュメントを取得する代わりに、「仮説的な」回答を生成してエンコードします。正しい答えを持つドキュメントは、質問よりも間違った答えに似ています。
- > [@goodside](https://twitter.com/goodside/status/1615383151987294209): Clever paper — [[HyDE]]: Hypothetical Document Embeddings
- > Instead of encoding the user's query to retrieve relevant documents, generate a "hypothetical" answer and encode that. Documents with right answers more similar to wrong answers than to questions. [https://t.co/Yayyu92Olu](https://t.co/Yayyu92Olu)
- > ![image](https://pbs.twimg.com/media/Fmr8uVYaEAEg_Ik.jpg)

以前[[blu3mo]]に教えてもらったテクニック、こういう名前がついていた
