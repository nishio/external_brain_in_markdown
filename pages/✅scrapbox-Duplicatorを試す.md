---
title: "✅scrapbox-Duplicatorを試す"
---

[tkgshn/scrapbox-Duplicator: Scrapboxの非公開・公開プロジェクトを分けて運用する際に面倒な「ページの転送」を自動で行うツール](https://github.com/tkgshn/scrapbox-Duplicator)を試す

[[✅Scrapbox Bot用のアカウントを作る]]

[tkgshn/scrapbox-Duplicator](https://github.com/tkgshn/scrapbox-Duplicator)に戻ってDeploy Herokuする
![image](https://gyazo.com/9971a5dc5b06ebf15343a825af573e6e/thumb/1000)
App nameは世界でユニークじゃないといけない

![image](https://gyazo.com/7952649d590a3d4a7a94d1d4df4968a6/thumb/1000)
ここにさっきメモしたSIDを入れる。
将来的には転送元プロジェクトは柔軟にしたいが、まあまずは実験。

デプロイ待ちの間にテストページを作っておく
![image](https://gyazo.com/47223c88ec45cca53dced30c585820f0/thumb/1000)

[/bluemountain-theme/ページ転送する拡張script](https://scrapbox.io/bluemountain-theme/ページ転送する拡張script)
あ、これはbodyに積むタイプか。長さ上限がどの程度なのか気になる。

`$ heroku run -a scrapbox-duplicator-nishio npm run transfer`
:

```
Running npm run transfer on ⬢ scrapbox-duplicator-nishio... up, run.1786 (Free)

> @ transfer /app
> node index.js

(node:21) UnhandledPromiseRejectionWarning: Error: Request failed with status code 403
  ...
```


うーん、よくわからないのでまずはローカルで動かすか
`$ git clone https://github.com/tkgshn/scrapbox-Duplicator.git`
`$ npm install`
`$ node --trace-warnings index.js`

ちゃんとボットアカウントでcsrfTokenを得てるがエクスポートのリクエストで失敗してるな…
あ、わかった、Scrapboxのエクスポートはプロジェクトのオーナーしかできないのか
- ![image](https://gyazo.com/da658fdcb7bc4444f91a10d4534f02ee/thumb/1000)
うーん、[[ページリストAPI]]で直近100件の投稿を取得する形に変えるかな

いや、インポートもオーナーだけか
- ![image](https://gyazo.com/5431a68fcc3ec46893e2e62ce30f41dc/thumb/1000)

自分のSIDを使ったらできた
![image](https://gyazo.com/8ac5358bc01b5918c68e2c8acea5a2dd/thumb/1000)![image](https://gyazo.com/678b95f9af743015291f5aecf2c4683b/thumb/1000)


> @blu3mo: サブアカウントにadmin権限を与えればエクスポート等できると思います!

なるほど！
![image](https://gyazo.com/28f7262a969ad465b184a30fa8fc838f/thumb/1000)

できたー！
![image](https://gyazo.com/65d6018a839bcb20352309744eb0fedf/thumb/1000)


memo
`waitFor is deprecated and will be removed in a future release. See https://github.com/puppeteer/puppeteer/issues/6214 for details and how to migrate your code.`
