---
title: "TTTCをAzure OpenAIで使う"
---

諸般の事情でTalk to the CityをOpenAIのAPIではなく[[Azure OpenAI Service]]でやることになった
- [Azure OpenAI Service – 高度な言語モデル | Microsoft Azure](https://azure.microsoft.com/ja-jp/products/ai-services/openai-service)

[[Talk to the City]] ScatterはLangChainのChatOpenAIをハードコードしている
extraction.py

```
llm = ChatOpenAI(model_name=model, temperature=0.0)
```


そこで[[Azure OpenAI]]で使うためにはここを書き換える必要がある

元々のコードでは`from langchain.chat_models import ChatOpenAI`とimportしている
素直に考えると`from langchain.chat_models import AzureChatOpenAI`にしたらすんなり動きそうだと思うよね
- LangChainは下部レイヤーを抽象化するためにミドルレイヤーとして挟まってるという期待
- だけどなんだかうまく動かなかった
    - 原因は特定できていないのでここが問題ではない可能性もある
最終的に`from langchain_openai import AzureChatOpenAI`にしたら動いた

修正箇所としてはこんな感じ
py

```
# llm = ChatOpenAI(model_name=model, temperature=0.0)
llm = AzureChatOpenAI(
    model_name=model, 
    temperature=0.0,
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    openai_api_key=os.getenv("AZURE_OPENAI_API_KEY"),
    openai_api_version=os.getenv("AZURE_OPENAI_API_VERSION"))
```

パラメータが増えたのでdotenvで`.env`を読んでる
py

```
import dotenv
import os
dotenv.load_dotenv()
```

`.env`に書く`AZURE_OPENAI_ENDPOINT`などの情報は「リソース」を作成して「モデル」をデプロイすればわかる
![image](https://gyazo.com/65f74e64e4b97696fd5abe034c27e721/thumb/1000)
![image](https://gyazo.com/0eb102394a58bfdb35d4d1108a4fbe8f/thumb/1000)
![image](https://gyazo.com/23a267e6425dd5da9279dcc21b62d6c6/thumb/1000)

AZURE_OPENAI_API_VERSIONが必要かと思って書いたけど、AZURE_OPENAI_ENDPOINTのquery parameterに積まれてるから省略してもいいのかもしれない

あと、これでいいかと思いきやEmbeddingだけモデルが別なのでそちらの作業もする必要がある
`from langchain_openai import AzureOpenAIEmbeddings`
py

```
embeds = AzureOpenAIEmbeddings(
    model="text-embedding-3-large",
    openai_api_key=os.getenv("AZURE_OPENAI_API_KEY"),
    openai_api_version=os.getenv("AZURE_OPENAI_API_VERSION")
).embed_documents(args)
```

なんでこっちはAZURE_OPENAI_ENDPOINTがないんだっけ
- あ`AZURE_EMBEDDING_ENDPOINT`をダイレクトに環境変数から読んでるのか
    - `.env`に`AZURE_EMBEDDING_ENDPOINT=https://<resource>.openai.azure.com/openai/deployments/text-embedding-3-large/embeddings?api-version=2023-05-15`とか書いてる


[[社内TTTC]]
