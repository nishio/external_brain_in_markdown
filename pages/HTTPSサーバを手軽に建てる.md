---
title: "HTTPSサーバを手軽に建てる"
---

ローカルでHTTPSサーバを建ててiframeで各種サービスを埋め込んでダッシュボード的にしたらいいんじゃないかという思考の過程で調べたもの
- 結果: [[HTTPSサービスを他のHTTPSサービスに埋め込む]]ことがサービスによってはヘッダーでブロックしていることがわかって諦めたので試してない


<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>
- ローカルでHTTPSサーバを構築する方法として、mkcertと[[Caddy]]が紹介されました。
- Caddyは自動でHTTPS証明書（Let’s Encryptなど）を取得し、シンプルなCaddyfileで設定可能です。
- ローカルで静的コンテンツを配信するための設定例として、
:

```
https://localhost {
 root * ./public
  file_server
 }
```

- を用い、`caddy run`でサーバを起動する方法が説明されました。

[https://chatgpt.com/c/67bf3ea3-eea0-8011-9939-626e8039770f](https://chatgpt.com/c/67bf3ea3-eea0-8011-9939-626e8039770f)

[Install — Caddy Documentation](https://caddyserver.com/docs/install)
