
> Access to fetch at '[http://localhost:5000/api/web/create'](http://localhost:5000/api/web/create') from origin '[http://localhost:3000'](http://localhost:3000') has been blocked by CORS policy: Response to preflight request doesn't pass access control check: Redirect is not allowed for a preflight request.

[オリジン間リソース共有 (CORS) - HTTP | MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)
[Preflight request (プリフライトリクエスト) - MDN Web Docs 用語集: ウェブ関連用語の定義 | MDN](https://developer.mozilla.org/ja/docs/Glossary/Preflight_request)

ブラウザはリクエストに先駆けてOPTIONSメソッドでリクエストを出している。
サーバがそのリクエストに対して308 Permanent Redirectを返していて、そのためCORS可能とはみなされない。

原因
- サーバ側
    - `@app.route('/api/web/create/', methods=["GET"])`
- クライアント側
    - `fetch(APIROOT + "web/create", {...})`
- これは末尾のスラッシュなしでのアクセスをありのURLにリダイレクトしてるのだな

解決
- `fetch(APIROOT + "web/create/", {...})`にしたら解消した

[[CORS]]
[[Flask-CORS]]
