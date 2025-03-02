
手元での開発にHTTPSをしゃべって欲しいケースがある
と思ってやり方を調べたけど
ローカル開発の時は[[webpack-dev-server]]もHTTPだから余計なお世話だった
(別の原因のエラーなのに早とちりした)
[[FlaskのHTTPS化]]

メモ

`$ openssl genrsa -aes128 1024 > server.key`
`$ openssl req -new -key server.key > server.csr`
CSR: Certificate Signing Request
`$ openssl x509 -in server.csr -days 365 -req -signkey server.key > server.crt`
CRT: Certificate
`$ flask run --cert server.crt --key server.key`
: 

```
 * Serving Flask app "server" (lazy loading)
 * Environment: development
 * Debug mode: on
 * Running on https://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: xxx-xxx-xxx
Enter PEM pass phrase:
```

これでHTTPSにすることはできるのだけど、コード編集の後の自動再起動で毎回パスフレーズを聞かれてしまうのでパスフレーズなしにした方が良さそう、今度必要になったら試す

memo
[Chromeでエラーにならない自己認証局＆サーバー証明書を作る – 走って登る](https://blog.liclab.com/2018-02-07/celf-signed-certificate/)