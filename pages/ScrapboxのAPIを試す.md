
- /api/pages/<project_name>
    - createdなどには整数が入っている
        - 秒単位のunixtimeだと思われる
        - [Date - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Date)
        - 1000倍して `new Date(x * 1000)` すれば日時が取れる
    - ログインしていなくても取れる
        - じゃあaccessedの値は何だよ…
- `No 'Access-Control-Allow-Origin' header is present on the requested resource.`
    - あれ？scrapbox.ioからしかアクセスを受け付けてない？

- [[Scrapboxのソート順序を変える実験]]
- [[ScrapboxAPI]]
