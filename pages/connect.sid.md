---
title: "connect.sid"
---

Scrapboxのログインが必要なAPIをスクリプトから叩くための認証情報

ブラウザでのログイン状態ではクッキーに認証情報がセットされる。これを使う。

このクッキーは[[Secure]]で[[HttpOnly]]なのでdocument.cookieを見てもわからない。
> To prevent cross-site scripting (XSS) attacks, HttpOnly cookies are inaccessible to JavaScript's Document.cookie API
- [HTTP cookies | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

Chrome Devtoolsだとここで見れる。
- ![image](https://gyazo.com/ce08d69ca4712edf038c17fb9f8f2bd2/thumb/1000)

具体的には"connect.sid"という名前で認証情報が入っている。例えば[[requests]]でAPIを呼び出す際にcookiesとして渡せば良い。
python

```
cookies={"connect.sid": "..."}
r = requests.get("https://scrapbox.io/api/pages/...", cookies=cookies) 
```


この情報は漏らさないように気をつける必要がある
- もし漏らしたなら、ログアウトしてログインし直したらリセットできる