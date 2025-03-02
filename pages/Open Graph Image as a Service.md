
[https://og-image.vercel.app/](https://og-image.vercel.app/)

PuppeteerにHTMLを渡してスクリーンショットを撮っている
- そのHTMLがFirestoreにアクセスしてデータを読んで描画するのを待たないといけない
- Firestoreへのアクセスがロード後に非同期で走るわけなのでそれを待つ手段が...
    - [https://pptr.dev/#?product=Puppeteer&version=v10.2.0&show=api-pagesetcontenthtml-options](https://pptr.dev/#?product=Puppeteer&version=v10.2.0&show=api-pagesetcontenthtml-options)
        - Puppeteer側のオプションでネットワーク接続が全部止まるまで待つことができる

- 文字列としてHTMLを生成して、setContentしてる
    - これはKozanebaと繋ぐの大変そう
    - サービスとして分離してgotoでやるのが良さそう

- ページのmetaタグをページロード後にJSで書き換えるような構成にしても各種SNSのクローラーは対応できない
- サーバサイドでHTMLを出しわけないといけない
- 個別のmetaのついた最小限のHTMLをサーバサイドで作って吐くところまでvercelでやればいいか…

キャッシュコントロール
- [https://vercel.com/docs/edge-network/caching](https://vercel.com/docs/edge-network/caching)
- [https://vercel.com/docs/serverless-functions/edge-caching](https://vercel.com/docs/serverless-functions/edge-caching)
