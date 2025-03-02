
実験的な機能をFlaskでサーバ立てて実験しようとした時に、そのサーバのAPIを別のサーバに置かれたコンテンツのJSで読み込もうとするとCORS policyでブロックされる。

:

```
Access to fetch at 'http://localhost:5000/api/' from origin 'http://localhost:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource. If an opaque response serves your needs, set the request's mode to 'no-cors' to fetch the resource with CORS disabled.
```


サーバサイド
- [[Flask]]-[[CORS]]を使う(`pip install -U flask-cors`)
    - [https://flask-cors.readthedocs.io/en/latest/](https://flask-cors.readthedocs.io/en/latest/)
diff

```
  from flask import Flask
+ from flask_cors import CORS

  app = Flask(__name__)
+ CORS(app)
```


クライアントサイド
diff

```
  fetch("http://localhost:5000/api/", {
+  mode: "cors",
   method: "POST",
    body: JSON.stringify(data),
    headers: {
      "Content-Type": "application/json",
    },
  }).then((response) => {
```


"Content-Type": "application/json"で叩いてるのでFlaskの側ではjsonで受ける
- これを忘れてて400 Bad Requestになった
- [[JSからFlaskを叩いて400 Bad Request]]

OPTIONSでの[[preflight requestが308 Permanent Redirect]]
- 原因は末尾のスラッシュ