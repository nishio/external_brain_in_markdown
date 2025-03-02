---
title: "my-tools"
---

自分の細々とした自動化ツールをAIエージェントも使えるようにするためのMCPサーバ
private [https://github.com/nishio/my-tools](https://github.com/nishio/my-tools)
public [https://github.com/nishio/my-tools-mcp-server-public-preview](https://github.com/nishio/my-tools-mcp-server-public-preview)


2025-02-03
MCPサーバを作る
`$ mkdir my-tools`
`$ code my-tools`

add a tool
![image](https://gyazo.com/7717f93b75e0462be4ecbfe7286fa51a/thumb/1000)
ローカルのPythonスクリプトを呼び出す実験として、呼び出したら現在時刻を返すものを作ろうと思う

MCPサーバーを作成
`$ npx @modelcontextprotocol/create-server time-server`
![image](https://gyazo.com/792ff0f0146383efe296bc993f010cf9/thumb/1000)

MCPサーバーはすでにビルドされているとのことですので、次のステップはこのサーバーにPythonスクリプトを呼び出すツールを追加することです。サーバーの設定ファイルを編集して、Pythonスクリプトを呼び出すツールを追加します。
index.ts

```typescript
{
  name: "get_current_time",
  description: "Get the current time",
  inputSchema: {
    type: "object",
    properties: {},
    required: []
  }
}
```

なるほど
index.ts

```typescript
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  switch (request.params.name) {
    case "get_current_time": {
      const { execSync } = require('node:child_process');
      const output = execSync('python3 current_time.py').toString().trim();
      return {
        content: [{
          type: "text",
          text: `Current time is: ${output}`
        }]
      };
    }

    default:
      throw new Error("Unknown tool");
  }
});
```

なるほど

![image](https://gyazo.com/9397c9b24c534d50c529db5fec707ebd/thumb/1000)

:

```
{
  "mcpServers": {
    "time-server": {
      "command": "node",
      "args": ["/Users/nishio/my-tools/time-server/build/index.js"],
      "env": {}
    }
  }
}
```


current_time.pyスクリプトが見つからないというエラーが発生しています。これは、スクリプトのパスが正しく指定されていないことが原因です。execSyncでスクリプトを実行する際に、正しいパスを指定する必要があります。time-server/src/index.tsファイルを修正して、current_time.pyの正しいパスを指定します。

![image](https://gyazo.com/3a91e72799336db50aecf8261f59ff20/thumb/1000)
できた！

![image](https://gyazo.com/31d89cd40a903e3d3687d2d8887c1f3d/thumb/1000)


Claude Desktop
![image](https://gyazo.com/05d47ace4d2c281ddeee0252ba078ae5/thumb/1000)
![image](https://gyazo.com/74a210bcf027356e5f02ac546d375ec3/thumb/1000)
できたできた

理屈はわかったので今後どうするかを考える
細々としたツールを作るたびに新しいサーバを作って設定するのは何だから、my-toolsというサーバに工具箱的に色々入れてる感じにしたい

`$ npx @modelcontextprotocol/create-server mcp-server`
で、time-serverの時間取得機能をmcp-serverに移す

できた。

このMCPサーバを汎用の「他の人も使うもの」として公開してメンテナンスするより、自分専用のものにして「自分はDropboxのここに論文を入れてる」とかの知識をコードとして言語化していった方が「僕+AIエージェント」としての生産性は高くなると思う
- 汎用のツールを使う人は結局その汎用のツールを自分の状況に合わせてカスタマイズするという「抽象度の高いシステム記述」をやることになる
- 僕個人が使う上で汎用化してから自分に特化させるのは二度手間だ
- 現状スクリプトも僕のユーザ名を含む絶対パスになってるしw
- というわけでprivate repoにpushしておいた
- 一方で現時点で特に秘密情報はないから、それは別途公開の方に入れておいた
