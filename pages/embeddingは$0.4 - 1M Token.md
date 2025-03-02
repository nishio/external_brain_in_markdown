
[Pricing](https://openai.com/pricing) [[Embedding API]]
> Model	Usage
>  Ada	$0.0004 / 1K tokens

大雑把にいえば1000人の社員が毎日平均1000文字をグループウェアに投稿しているような会社で、全発言をembeddingした場合、1日200円弱になる。

平均10投稿だとすると1日60MBのベクトルインデックスが作られるのでPinecoreの従量課金は0.05ドル、ランニングコストは1000円くらいか

[New and improved embedding model](https://openai.com/blog/new-and-improved-embedding-model)
2022-12-15 `text-embedding-ada-002`がbest
- context length: 8192
- 1536 dimensions
    - 1/8のサイズにしたけど、それでも才能が上がったらしい

[OpenAI API:what-are-embeddings](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings)
- [[cl100k_base]]はトークナイザの名前
    - > For second-generation embedding models like text-embedding-ada-002, use the cl100k_base encoding.
    - [[tiktoken]]
- [[Pinecore]]
