
[OpenAI API](https://platform.openai.com/docs/guides/embeddings/what-are-embeddings)のサンプルコードではこんなことが書いてある
python

```
def get_embedding(text, model="text-embedding-ada-002"):
   text = text.replace("\n", " ")
   return openai.Embedding.create(input = [text], model=model)['data'][0]['embedding']
```


空白と改行自体は異なるトークンになっているのに、なぜ置換が必要なのか？本当に必要なのか？と疑っていたが、置き換えた方が結果が良くなるからだという記述があった。
- > Replace newlines with a single space
- >  Unless you're embedding code, we suggest replacing newlines (\n) in your input with a single space, as we have observed inferior results when newlines are present.
    - [How to generate embeddings with Azure OpenAI Service - Azure OpenAI | Microsoft Learn](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/embeddings?tabs=console)

追試はしていない
- 日本語でもそうなのかは怪しい
- が、まあ従っておこうかなという気持ち

[[OpenAI API]]
