---
title: "✅最新のChromeで画像付箋が表示されない"
---

[[pRegroup-done]]
まとめ
- ChromeがHTTPSのページからHTTPの画像を読まなくなった
- 画像は[[キャンバス汚染]]の解決のためにヘッダをいじる必要があり、EC2で立てたプロキシサーバを通していた、これがHTTPであった
- サーバをherokuに移して解決
    - herokuがgunicornにワイルドカード証明書を使っている
    - 自分で証明書を取ってgunicornを挟んでEC2でやるのでもOKのはず

---
現象
- PCで画像付箋が表示されない
- PCでScrapbox付箋のアイコンが表示されない

参考
- [[付箋に画像を表示]]
    - > EC2-nanoでプロキシ立てた

このプロキシがHTTPだが、最新のChromeはもはやHTTPSのページからHTTPへのリクエストを許さない
- `Mixed Content: The page at 'https://...' was loaded over HTTPS, but requested an insecure element 'http://...'. This request was automatically upgraded to HTTPS, For more information see`
- [Chromium Blog: No More Mixed Messages About HTTPS](https://blog.chromium.org/2019/10/no-more-mixed-messages-about-https.html)
    - > This feature will autoupgrade optionally-blockable mixed content (HTTP content in HTTPS sites) by rewriting the URL to HTTPS, without a fallback to HTTP if the content is not available over HTTPS. Image mixed content autoupgrades by default are targeted for M86.
    - 今までは画像に関してはデフォルトではオートアップグレードしなかったが、M86からするように変わった。このオートアップグレードはHTTPにフォールバックしないのでHTTPのみでサーブされてる画像は表示不能になる。
    - → net::ERR_SSL_PROTOCOL_ERROR
- Chrome M86から
- [サーバーでの HTTPS の有効化  |  Web  |  Google Developers](https://developers.google.com/web/fundamentals/security/encrypt-in-transit/enable-https)

解決方法案
- Flaskで書いたサーバをHTTPSにする
    - [rest - can you add HTTPS functionality to a python flask web server? - Stack Overflow](https://stackoverflow.com/questions/29458548/can-you-add-https-functionality-to-a-python-flask-web-server)
- 他の方法
    - AWS Lambdaとか？
    - 手前にcloudflareを置く
- なぜLambdaじゃないのだっけ？
    - [[AWS Lambdaで画像プロキシを動かす]]
    - バイナリデータを返すのが手間だったから
- herokuに置いたAPIサーバは問題なく動いてる、なぜ？
    - gunicornを挟んでいるのでそこでHTTPSになる
