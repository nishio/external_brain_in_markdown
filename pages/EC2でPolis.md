
まとめ
- 適当に Ubuntu / t2.medium / 8GB でインスタンスを作る
- Dockerをインストール
- Polisをインストール
    - localhost以外で動かすならSSL証明書が必要


log on 2023-05-22
適当に Ubuntu / t2.micro / 8GB でインスタンスを作る
- インスタンスを起動したらすぐブラウザ上からターミナルに接続できる風の画面が出て「べんりになったんだなー」と思ってクリックしたらインスタンスが起動中だから接続できなくてズッコケた

Dockerをインストール
- [Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)
- Hello world: OK

Polisをインストール
- [GitHub - compdemocracy/polis: Open Source AI for large scale open ended feedback](https://github.com/compdemocracy/polis)
- `$ git clone https://github.com/compdemocracy/polis.git`
- `$ sudo apt install make`
- READMEに従う
- `$ cp example.env .env`
- `$ make start`
    - `docker compose -f docker-compose.yml -f docker-compose.dev.yml --env-file .env up`
    - ERROR: `permission denied while trying to connect to the Docker daemon ...`
    - <img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/>
        - Dockerのデーモンはrootユーザーとして実行され、デフォルトでは他のユーザーはそれと対話できません。これが"permission denied"エラーが表示される理由です。
        - この問題を解決するためには以下の手順を試してみてください：
            - ユーザーをdockerグループに追加する：これがこの問題を解決するための推奨される方法です。以下のコマンドでユーザーをdockerグループに追加できます：
            - `$ sudo usermod -aG docker $USER`
        - このコマンドを実行した後、グループのメンバーシップを再評価するためにログアウトして再度ログインする必要があります。
    - 直った！

10分経ってもビルドが終わらない
- t2.microは小さすぎたか
- t2.mediumにしてみよう
- [Amazon EC2 T2 インスタンス | AWS](https://aws.amazon.com/jp/ec2/instance-types/t2/)

SSL証明書
- ![image](https://gyazo.com/c0e9f95d8c7b2a598a88e4aaa860b009/thumb/1000)
- > メインREADMEで説明されているDocker Composeインフラストラクチャは、安全でない自己署名SSL証明書を使用しています。これは事前に生成され、ソースコードに公開されて保存されています。このHTTPSの実装は、テストにのみ適しています。
    - [polis/ssl.md at edge · compdemocracy/polis · GitHub](https://github.com/compdemocracy/polis/blob/edge/docs/ssl.md)
- 後でやる

create account
- ERROR: `unauthorized domain: https://3.87.68.32`
server.ts

```typescript
if (
  !domainOverride &&
  !hasWhitelistMatches(host) &&
  !routeIsWhitelistedForAnyDomain
) {
  logger.info("not whitelisted", { headers: req.headers, path: req.path });
  return next("unauthorized domain: " + host);
}
```

- `.env`
    - ![image](https://gyazo.com/a8cdf4dc6d10f29fc4c0ddc4a109dc70/thumb/1000)
- localhostではないから、この辺の設定をやる必要があるのか
- できた
    - ![image](https://gyazo.com/8ad5ca4a532c28ff9da40035e9309f92/thumb/1000)

SSL証明書
- 自分が管理してるDNSにAレコードを追加
- nslookupでちゃんと引けることを確認
- ブラウザでアクセスしてみる
    - > このサイトにアクセスできません DNS_PROBE_FINISHED_NXDOMAIN
    - <img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/>Local DNS Cache: Your computer stores a local DNS cache to speed up the resolution of domain names. If this cache is outdated or corrupt, it can cause this error. You can clear your local DNS cache with the following command ...
        - (OSX) `% sudo killall -HUP mDNSResponder`
    - ERR_CONNECTION_REFUSEDに変わった
        - あ、サーバ起動してなかった
- Let's Encryptのcertbotは80を使うのでPolisのサーバを建てた状態ではダメ
:

```
Certbot failed to authenticate some domains (authenticator: standalone). The Certificate Authority reported these problems:
  Domain: *****
  Type:   dns
  Detail: DNS problem: NXDOMAIN looking up A for ***** - check that a DNS record exists for this domain; DNS problem: NXDOMAIN looking up AAAA for ***** - check that a DNS record exists for this domain
```

- DNSのせいかと思って少し待ったりしてたが、違うなこれ
    - EC2のセキュリティルールで443と22しか開けてなかった
    - 80番を開けて、外からアクセスできることを確認
        - `$ sudo python3 -mhttp.server 80`
- > [@nishio](https://twitter.com/nishio/status/1660488886341234690?s=20): SSL証明書の作り方とかよくわからない素人質問なんですけど、30分ほど前に新しくDNSにAレコードを書き足したサブドメインに対してLet's Encryptで証明書を作ろうとしてNXDOMAINエラーになるのって、しばらく待つしかないんですかね
    - (単純にドメイン名を間違えてただけかもorz)

証明書ができた
`file-server/nginx.Dockerfile`と`file-server/nginx/nginx-ssl.site.default.conf`をいじる
- `nginx-ssl.site.default.conf`はコピーした
diff

```
--- a/file-server/nginx.Dockerfile
+++ b/file-server/nginx.Dockerfile
@@ -1,10 +1,12 @@
 FROM docker.io/nginx:1.21.5-alpine
 
-COPY nginx/nginx-ssl.site.default.conf /etc/nginx/conf.d/default.conf
+COPY nginx/nginx-ssl.site.nhiro.conf /etc/nginx/conf.d/default.conf
 
 # We only use these in testing.
 COPY nginx/certs/snakeoil.cert.pem /etc/nginx/certs/snakeoil.cert.pem
 COPY nginx/certs/snakeoil.key.pem  /etc/nginx/certs/snakeoil.key.pem
+COPY fullchain.pem /etc/nginx/certs/fullchain.pem
+COPY privkey.pem /etc/nginx/certs/privkey.pem
```

conf.diff

```
     server_name _;
 
-    ssl_certificate /etc/nginx/certs/snakeoil.cert.pem;
-    ssl_certificate_key /etc/nginx/certs/snakeoil.key.pem;
+    ssl_certificate /etc/nginx/certs/fullchain.pem;
+    ssl_certificate_key /etc/nginx/certs/privkey.pem;
     ssl_session_timeout 10m;
```

- `$ docker compose up --detach --build --no-deps nginx-proxy`
    - [https://gist.github.com/nishio/917ae036c22c55fc4763d6864898aa5c](https://gist.github.com/nishio/917ae036c22c55fc4763d6864898aa5c)
- 本当はLet's encryptのcertbotが自動更新するみたいなので証明書ファイルをその置かれてる場所から取ってくるのがよいが、面倒なのでcpした
    - ファイルの置き場所や、ディレクトリやファイルの所有者がrootであること、パーミッションなどの影響で読み込めなかった場合に、わかりやすくエラーが出て止まるのではなく単にサーバに繋がらなくなる、何が原因かを調べるのがめんどくさかった
    - 最終的に証明書をsudo cpしただけだとダメでchmod 666したら動いた


しばらく経ったらBad Gatewayで死んでた
`polis-dev-nginx-proxy-1  | 2023/05/24 04:16:35 [error] 32#32: *12492 connect() failed (111: Connection refused) while connecting to upstream, client: ::ffff:133.200.136.32, server: _, request: "GET /7xrm9snjcc HTTP/2.0", upstream: "http://172.18.0.5:5000/7xrm9snjcc", host: "polis.nhiro.org", referrer: "https://t.co/"`
うーん、nginxの先で死んでるのか
開発の観察目的で開発サーバをそのまま本番運用しているのでアクセスが集中するとダメなのかもな
原因究明のためにログを見ると良さそう、どこだろ

詳細レポート表示がエラーになる
- > GET /report/undefined/api/v3/reports?report_id=r2bafdsneascdm6sbmnad 404
    - `undefined`
- レポート画面だけ.envからURLのプレフィックスを読んでる
- 指摘されてないときにdocument.originを代わりに使っているが、それがundefined



from [/villagepump/2023/05/24](https://scrapbox.io/villagepump/2023/05/24)
<img src='https://scrapbox.io/api/pages/villagepump/inajob/icon' alt='/villagepump/inajob.icon' height="19.5"/>
- UIが同じなので、ログインできてないのを謎に感じた（当然なのだけど）
- ログイン導線のリンクをクリックすると本家の[[Polis]]に飛ばされるので、混乱した
- [[Twitter連携]]が出来ない（キーの設定をしていない？）
    - してないかも！<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
        - 意見投稿が匿名でできるようにしてある、管理者の作ったシード意見と参加者の投稿した意見は区別つかなくなってます
- 経緯: 社内で発生した議論をPolisにつっこみたかった<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
    - pol.isは「外部クラウドサービス」扱いになるので面倒
        - サクッと立てて社内の目的で使う手順がわかりやすくなれば世の中のために有益だと思う<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
            - 特に僕は「これ民間企業内の意思決定にも有益では？」と思ってるので。
--
[[polis]]ってログインせずに投票できたんだ<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
- 投票して離れると自分の投票結果をロストしてしまう。どうしたらいいのかわからない<img src='https://scrapbox.io/api/pages/villagepump/issac/icon' alt='/villagepump/issac.icon' height="19.5"/>
    - 連携するツイッターがないので、アイコンからも遡れない
        - 自分が投票したという記憶のみが残る
    - 連携しても各質問のどれに答えたかは見ることができない（はず）<img src='https://scrapbox.io/api/pages/villagepump/inajob/icon' alt='/villagepump/inajob.icon' height="19.5"/>
        - 過去に答えた投票一覧などもない（欲しい）
        - 図が出たときにアイコンが自分のものになるのと、追加質問があったときにメール通知が来るだけという理解
        - 色々いじっていきたい(そのための自前インスタンス)<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
