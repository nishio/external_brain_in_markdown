---
title: "pVectorSearch2023-06-05"
---

prev [[pVectorSearch2023-06-02]] parent [[pVectorSearch]]

NextJS
- [Getting Started: Installation | Next.js](https://nextjs.org/docs/getting-started/installation)
    - `$ npx create-next-app@latest`
    - TypeScript使いますかとか聞いてくれる
    - `vecsearch-service`って名前にした
    - この名前のフォルダが作られてGit管理される
- Githubに入れる
    - > push an existing repository from the command line
    - privateにした

Vercel
- ダッシュボードにログインする
- 先ほどのリポジトリが表示されてるので選んでデプロイ
- デプロイできた
- あー、`https://vecsearch-service.vercel.app/`になるのか
- 設定からすぐ変えられる
    - [https://nishio-vecsearch.vercel.app/](https://nishio-vecsearch.vercel.app/)
便利な時代だなぁ

APIを作る
- [Routing: API Routes | Next.js](https://nextjs.org/docs/pages/building-your-application/routing/api-routes)
- `src`がないときの置き場所は、`<project_root>/pages/api/foo.ts`
ts

```typescript
import { NextApiRequest, NextApiResponse } from "next";

const handle = async (_req: NextApiRequest, res: NextApiResponse) => {
  res.status(200).json({ data: "hello world" });
};
export default handle;
```

- OK
- うまく動かなくて混乱したがGPT-4に聞いたら「サーバを再起動してみろ」と言われたので再起動したら動いた、便利な時代

他のAPIを叩くAPI
- とりあえずScrapboxAPIで試す
    - [https://scrapbox.io/api/pages/nishio/pVectorSearch2023-06-05](https://scrapbox.io/api/pages/nishio/pVectorSearch2023-06-05)
ts

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import axios from "axios";

const handle = async (_req: NextApiRequest, res: NextApiResponse) => {
  const otherApiUrl =
    "https://scrapbox.io/api/pages/nishio/pVectorSearch2023-06-05";

  try {
    const response = await axios.get(otherApiUrl, {});
    res.status(200).json(response.data);
  } catch (error) {
      res
        .status(500)
        .json({ error: "An error occurred while calling the other API" });
  }
};
export default handle;
```

    - OK

OpenAIを叩く
embed.ts

```typescript
import axios from "axios";

export const embed = async (textToEmbed: string) => {
  const model = "text-embedding-ada-002";
  const URL = "https://api.openai.com/v1/embeddings";
  // Call OpenAI Embedding API
  const openAIResponse = await axios.post(
    URL,
    { input: textToEmbed, model: model },
    {
      headers: {
        Authorization: `Bearer ${process.env.OPENAI_API_KEY}`,
        "Content-Type": "application/json",
      },
    }
  );
  const openAIEmbedding = openAIResponse.data.data[0].embedding; // assuming the embedding is in this path
  return openAIEmbedding;
};
```

embed.ts

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import { embed } from "../../utils/embed";

const handle = async (req: NextApiRequest, res: NextApiResponse) => {
  const textToEmbed = req.body.text;
  const openAIEmbedding = await embed(textToEmbed);
  res.status(200).json(openAIEmbedding);
};
export default handle;
```

- OK

Qdrantを叩く
search.ts

```typescript
import { NextApiRequest, NextApiResponse } from "next";
import { embed } from "../../utils/embed";
import { QdrantClient } from "@qdrant/js-client-rest";

const handle = async (req: NextApiRequest, res: NextApiResponse) => {
  const textToEmbed = req.body.text;
  const openAIEmbedding = await embed(textToEmbed);

  const COLLECTION_NAME = process.env.QDRANT_COLLECTION_NAME!;

  const client = new QdrantClient({
    url: process.env.QDRANT_ENDPOINT,
    apiKey: process.env.QDRANT_API_KEY,
  });

  const grdantResult = await client.search(COLLECTION_NAME, {
    vector: openAIEmbedding,
    limit: 3,
  });

  res.status(200).json(grdantResult);
};
export default handle;
```

- OK

フォームから検索文字列を取る
:

```
Error: Event handlers cannot be passed to Client Component props.
 <button id="search" onClick={function} children=...>
                             ^^^^^^^^^^
If you need interactivity, consider converting part of this to a Client Component.
```


レスポンスを整形する
- ScrapboxのタイトルからURLを作る
- ![image](https://gyazo.com/27e93ce643025450fc3930f36cbffb46/thumb/1000)
- 見た目はさておき、検索はできた
    - タイトルをクリックするとScrapboxの該当ページにジャンプする
    - TailwindCSSが初めてなので見た目をどうするかわからない
        - ChatGPTに聞こうw
    - Make the result looks better.って言ったらいい感じにしてくれたw
        - ![image](https://gyazo.com/91e36c13c5d7e4a50e292b8fea06ab4e/thumb/1000)
    - 全体的に直させた
        - ![image](https://gyazo.com/05926e6fbdd4634d05ea0e3e899b86d7/thumb/1000)
        - こだわりがないウェブアプリの外見デザインに関してはChatGPTで十分だな…

次回のためのメモ
- ページタイトル画像
    - `/api/pages/:projectName/:pageTitle/icon`

- 管理者用の画面
    - 検索クエリは保管して管理者が見れるようにする
        - そういう旨の説明が書いてあるページを作る
        - 検索した時点で結果をFirebaseに入れてパーマリンクを出すか
    - 公開する
        - 自分でスマホから使ってみたりする
        - スマホから見たら背景が黒くなかった
        - 検索したときに、検索中なのかエラーで死んだのかわからない ✅fixed
        - スマホでエラーになる件 ✅fixed
            - 環境変数の設定し忘れ！
            - .env.localはデプロイ先の環境変数に入らない(そもそも.gitignoreしててリポジトリに入ってない！)
    - [[URL Fragment Text Directives]]をつける
        - これ厄介だな
            - 例えばScrapbox記法が混じってるとブラウザのテキストには記法がないからヒットしない
            - 真面目にやるならプレーンテキストにする必要がある

[GPT](https://chat.openai.com/share/a0afa341-a147-4c0f-a164-9587eb4fc815)
next: [[pVectorSearch2023-06-06]]

[[ベクトル検索で関連ページ]]