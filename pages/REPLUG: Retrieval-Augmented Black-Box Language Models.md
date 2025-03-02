
> We introduce [[REPLUG]], a retrieval-augmented language modeling framework that treats the language model (LM) as a black box and augments it with a tuneable retrieval model. Unlike prior retrieval-augmented LMs that train language models with special cross attention mechanisms to encode the retrieved text, REPLUG simply prepends retrieved documents to the input for the frozen black-box LM. This simple design can be easily applied to any existing retrieval and language models. Furthermore, we show that the LM can be used to supervise the retrieval model, which can then find documents that help the LM make better predictions. Our experiments demonstrate that REPLUG with the tuned retriever significantly improves the performance of GPT-3 (175B) on language modeling by 6.3%, as well as the performance of Codex on five-shot MMLU by 5.1%.
[https://arxiv.org/abs/2301.12652](https://arxiv.org/abs/2301.12652)
(DeepL)言語モデル（LM）をブラックボックスとして扱い、それを調整可能な検索モデルで補強する、検索補強型言語モデルフレームワークであるREPLUGを紹介する。検索されたテキストを符号化するために特別なクロスアテンションメカニズムを用いて言語モデルを学習する先行する検索補強型LMとは異なり、REPLUGは単に検索された文書を凍結されたブラックボックスLMの入力に追加するだけである。このシンプルな設計は、既存の検索モデルや言語モデルに容易に適用できる。さらに、LMを検索モデルのスーパービジョンに用いることで、LMがより良い予測を行うための文書を見つけることができることを示す。我々の実験では、チューニングされたレトリーバを持つREPLUGが、GPT-3(175B)の言語モデリングの性能を6.3%向上させ、Codexの5ショットMMLUの性能を5.1%向上させることを実証した。

[REPLUG: Retrieve and Plug – arXiv最新論文の紹介](https://devneko.jp/wordpress/?p=2884)

[[RAG]]: [[Retrieval-Augmented Generation]]
- [[Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks]]では内部状態に入れてるけど、プロンプトに付与するのもRAGとしてよい理由は？という疑問を持ってた
