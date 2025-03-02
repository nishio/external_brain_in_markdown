
[[connect.sid]]の話
- privateプロジェクトに限らないので整理したい
- だがあちこちからリンクされているので、このページは存続させることにした(2023-08-09)

2018-12-17
publicプロジェクトのAPIは単純にGETすればデータが得られるが、privateプロジェクトでそれをやると401になる。(当たり前)

ログイン状態でprivateプロジェクトにアクセスすると、クッキーに認証情報がセットされる。これを使う。

このクッキーは[[Secure]]で[[HttpOnly]]なのでdocument.cookieを見てもわからない。
> To prevent cross-site scripting (XSS) attacks, HttpOnly cookies are inaccessible to JavaScript's Document.cookie API
- [HTTP cookies | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)

Chrome Devtoolsだとここで見れる。
- ![image](https://gyazo.com/ce08d69ca4712edf038c17fb9f8f2bd2/thumb/1000)

具体的には"connect.sid"という名前で認証情報が入っている。これを例えば[[requests]]に渡せば良い。
python

```
cookies={"connect.sid": "..."}
r = requests.get("https://scrapbox.io/api/pages/...", cookies=cookies) 
```


このconnect.sidは2018年の今時点で2020年までexpiresしないやつなので当面アクセスできる。
もしうっかりこの情報を漏らしてしまった場合にリセットする方法があるかどうかは知らないので気をつける必要がある。
- ログアウトしてログインし直したら変わってた

thanks moriyoshi

[[ScrapboxAPI]] [[Scrapbox]]
