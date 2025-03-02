---
title: "2024年夏Polis祭り:インスタンスの準備"
---

from [[2024年夏Polis祭り]]
2024年夏Polis祭り:インスタンスの準備

2024-06-18

前回の記事を見る: [[EC2でPolis]]
- 適当に Ubuntu / t2.medium / 8GB でインスタンスを作る


前回はダイレクトにcloneしたが、今回はforkする
    - UIを日本語化するなのするかもなので
- [GitHub - compdemocracy/polis: :milky_way: Open Source AI for large scale open ended feedback](https://github.com/compdemocracy/polis)
- ![image](https://gyazo.com/59cc15bdfd0b814b53dc798d337cd407/thumb/1000)
- なんだこれ？
    - わからんのでデフォルトにしよう
- [https://github.com/nishio/polis](https://github.com/nishio/polis)
    - ![image](https://gyazo.com/f67f3503e112a32eaad59e85e5d981b1/thumb/1000)
        - ふむ

そうこうしているうちにインスタンスは起動した
![image](https://gyazo.com/00f7959982e7d683ba30c9434fa8ce5c/thumb/1000)![image](https://gyazo.com/047782a83e3b394c143f62e1f7d9d9cf/thumb/1000)

Dockerをインストール
- [Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)
- Hello world: OK


# Polisをインストール
`$ cp example.env .env`
`$ make start`
:

```
docker compose -f docker-compose.yml -f docker-compose.dev.yml --env-file .env up
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.45/containers/json?all=1&filters=%7B%22label%22%3A%7B%22com.docker.compose.config-hash%22%3Atrue%2C%22com.docker.compose.project%3Dpolis-dev%22%3Atrue%7D%7D": dial unix /var/run/docker.sock: connect: permission denied
make: *** [Makefile:34: start] Error 1
```

えっと
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>このエラーは、現在のユーザーがDockerデーモンソケットにアクセスする権限を持っていないために発生しています。
- `$ sudo usermod -aG docker $USER`
- `$ newgrp docker`
ビルドが動き出した
- なんらログが流れまくってるんだけど、ビルド終わってサーバが動いてるのかビルド中なのかよくわからないんだよな
- `http://<IP>/createuser`
    - 動いてた
    - ![image](https://gyazo.com/e64501b8e819a3cb978a668dfddb172e/thumb/1000)
- アカウント作成をすると
:

```
server-1       | info: not whitelisted  ... ,"path":"/api/v3/auth/new","service":"polis-api-server","timestamp":"2024-06-18 08:07:22 +00:00"}
server-1       | POST /api/v3/auth/new 500 160.657 ms - 40
server-1       | unauthorized domain: http://<IP>
```

- 前回もそうだった
    - ホワイトリストに入ってないからだ
    - HTTPなのと、IP丸だしなのと、問題だよね
    - そもそもこれは開発モードであった
- PRODにしてみる
    - `$ cp example.env prod.env`
    - `$ make PROD start`
    - アクセスはできた

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
1. ドメインの取得と設定
2. Let's EncryptでSSL証明書を取得
3. Nginxの設定
    - Nginxを使ってリバースプロキシを設定し、HTTPS対応にします。

えー、めんどくさそう<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
1. AWS Elastic Beanstalk
- メリット:
    - 簡単なデプロイ: コードをアップロードするだけで、自動的にインフラが構築される。
    - 管理の手間削減: 環境のスケーリングやロードバランシング、モニタリングなどが自動化される。
    - 統合: ACMと統合されており、簡単にHTTPS証明書を適用できる。
- デメリット:
    - 制限: 高度なカスタマイズが必要な場合には制約がある。
    - コスト: 他の方法と比べるとやや高くなる可能性がある。
2. AWS Fargate
- メリット:
    - サーバーレス: インフラ管理の手間が省ける。
    - スケーラビリティ: 自動でスケーリングされるため、高トラフィックにも対応可能。
    - 柔軟性: ECSクラスタを利用するため、詳細な設定やカスタマイズが可能。
- デメリット:
    - 学習コスト: 初期設定や理解に多少の時間がかかる。
    - コスト: 使用量に応じて料金が発生するため、継続的なコスト管理が必要。
3. AWS Lightsail
- メリット:
    - 簡単な設定: 初心者向けのインターフェースで、設定が非常に簡単。
    - 定額料金: 料金体系がわかりやすく、予算管理がしやすい。
    - 統合: SSL証明書の設定が簡単で、ロードバランサーの利用も容易。
- デメリット:
    - 制限: 高度なスケーリングや複雑なインフラ設定には向いていない。
    - 柔軟性: 他のAWSサービスに比べるとカスタマイズ性が低い。
まとめ
- AWS Elastic Beanstalk: 簡単にデプロイしたいが、多少の制限を受け入れられる場合に最適。
- AWS Fargate: 柔軟性とスケーラビリティが必要だが、初期設定の学習コストを受け入れられる場合に最適。
- AWS Lightsail: 初心者で、簡単かつコストを抑えたい場合に最適。
それぞれの方法には利点と欠点があり、具体的な要件や予算に応じて最適な方法を選ぶことが重要です。

どれがいいのか全然わからんw<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- GPT4、まかせた！
    - →Let's Encrypt + Nginx 路線
    - 判断つかないからそれでやるよ

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>サブドメインのDNSレコードを追加
- 「nhiro.org」のDNS設定を開き、以下のように「polis.nhiro.org」をEC2インスタンスのIPアドレスに向けるためのAレコードを追加します。
    - ホスト名（Host Name）: polis
    - タイプ（Type）: A
    - TTL: 600（またはデフォルト値）
    - 値（Value）: EC2のパブリックIPアドレス

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>DNSが更新されたかどうかを確認するためには、以下の方法を使います。
- nslookup
- dig

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>DNSの設定が正しく反映されていないようです。以下のステップを確認してみてください。
2. DNSキャッシュのクリア
    - macOS
        - `$ sudo killall -HUP mDNSResponder`

おっ、更新された<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
Nginxのインストール
`$ sudo apt update`
`$ sudo apt install -y nginx`
Nginxの設定ファイルを編集
`$ sudo vi /etc/nginx/sites-available/default`
:

```
server {
    listen 80;
    server_name your_domain.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name your_domain.com;

    ssl_certificate /etc/letsencrypt/live/your_domain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/your_domain.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```


viだと画面が壊れた、nanoならOK<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

Certbotのインストール
`$ sudo apt install -y certbot python3-certbot-nginx`
SSL証明書の取得
`$ sudo certbot --nginx -d polis.nhiro.org`

:

```
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Error while running nginx -c /etc/nginx/nginx.conf -t.

2024/06/18 08:59:32 [emerg] 12342#12342: cannot load certificate "/etc/letsencrypt/live/your_domain.com/fullchain.pem": BIO_new_file() failed (SSL: error:80000002:system library::No such file or directory:calling fopen(/etc/letsencrypt/live/your_domain.com/fullchain.pem, r) error:10000080:BIO routines::no such file)
nginx: configuration file /etc/nginx/nginx.conf test failed

The nginx plugin is not working; there may be problems with your existing configuration.
The error was: MisconfigurationError('Error while running nginx -c /etc/nginx/nginx.conf -t.\n\n2024/06/18 08:59:32 [emerg] 12342#12342: cannot load certificate "/etc/letsencrypt/live/your_domain.com/fullchain.pem": BIO_new_file() failed (SSL: error:80000002:system library::No such file or directory:calling fopen(/etc/letsencrypt/live/your_domain.com/fullchain.pem, r) error:10000080:BIO routines::no such file)\nnginx: configuration file /etc/nginx/nginx.conf test failed\n')
```


<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>このエラーは、Let's Encryptの証明書が存在しないため、Nginxが設定をロードできないことを示しています。
あるわけないだろ！！<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Nginxの設定からSSL部分を一時的にコメントアウトします。

:

```
$ sudo certbot --nginx -d polis.nhiro.org
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Enter email address (used for urgent renewal and security notices)
 (Enter 'c' to cancel): nishio.hirokazu@gmail.com 

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.4-April-3-2024.pdf. You must agree in
order to register with the ACME server. Do you agree?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y
Account registered.
Requesting a certificate for polis.nhiro.org

Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/polis.nhiro.org/privkey.pem
This certificate expires on 2024-09-16.
These files will be updated when the certificate renews.
Certbot has set up a scheduled task to automatically renew this certificate in the background.

Deploying certificate
Successfully deployed certificate for polis.nhiro.org to /etc/nginx/sites-enabled/default
Congratulations! You have successfully enabled HTTPS on https://polis.nhiro.org

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

できたらしい？

:

```
$ sudo systemctl restart nginx
Job for nginx.service failed because the control process exited with error code.
See "systemctl status nginx.service" and "journalctl -xeu nginx.service" for details.
```


:

```
Jun 18 09:04:06 ip-172-31-37-50 nginx[12385]: 2024/06/18 09:04:06 [emerg] 12385#12385: cannot load certificate "/etc/letsencrypt/live/your_domain.com/fullchain.pem": BIO_new_file() failed (>
Jun 18 09:04:06 ip-172-31-37-50 nginx[12385]: nginx: configuration file /etc/nginx/nginx.conf test failed
```

あー、`certificate "/etc/letsencrypt/live/your_domain.com/fullchain.pem"`
- `your_domain.com`がのこってたか

`$ sudo systemctl restart nginx`
- 今度は何も言わない、成功か？

Polisを起動する
:

```
Error response from daemon: driver failed programming external connectivity on endpoint polis-dev-nginx-proxy-1 (432b7de15349df46efb04a246102c6e420b7fdd790f2d3580a4ad0afc313a5cd): Error starting userland proxy: listen tcp4 0.0.0.0:443: bind: address already in use
```

あ〜〜〜

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
まず、ポート443がどのプロセスによって使用されているか確認します。
- `$ sudo lsof -i :443`
まあ普通にnginxだな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

ポート443を使用しているプロセスが不要なものであれば、停止します。例えば、Nginxが既に動作している場合、停止します。
`$ sudo systemctl stop nginx`

ポートが解放されたら、再度Nginxコンテナを起動します。

今度はちゃんと動いてそうだがブラウザからアクセスすると反応がない…はっ、これはあれだな！
![image](https://gyazo.com/426f81bb560937f83463a1298af31a82/thumb/1000)
443があいてない
- このミス人生で100回やった(誇張)

![image](https://gyazo.com/f213f68acb74c12ef23164f7b24a7ea1/thumb/1000)
えー、なんで
![image](https://gyazo.com/4c7ea8af3dc9a8dbe33e0aca9e940f98/thumb/1000)
なんで無効？
![image](https://gyazo.com/27c8b19fe6415a83505e6f34882f8cbb/thumb/1000)
え〜〜〜

〜〜〜

あ、Polis側のドキュメントでデフォルトではテスト用の証明書になってるって記述があった記憶が！
Polis側での設定変更が必要なんだな
[polis/docs/ssl.md at edge · nishio/polis](https://github.com/nishio/polis/blob/edge/docs/ssl.md)
書き換える
`$ sudo systemctl restart nginx`

:

```
$ sudo nginx -t
2024/06/18 14:18:04 [warn] 53602#53602: conflicting server name "polis.nhiro.org" on 0.0.0.0:443, ignored
```


:

```
ubuntu@ip-172-31-37-50:~/polis$ grep -r "server_name polis.nhiro.org" /etc/nginx/
/etc/nginx/sites-available/default:    server_name polis.nhiro.org;
/etc/nginx/sites-available/default:    server_name polis.nhiro.org;
/etc/nginx/sites-available/default:    server_name polis.nhiro.org;
ubuntu@ip-172-31-37-50:~/polis$ grep -r "server_name polis.nhiro.org" .
./file-server/nginx/nginx-ssl.site.default.conf:    server_name polis.nhiro.org;
```


nginx.Dockerfileのなかで設定ファイルをコピーしている
[[EC2でPolis#646c4176aff09e0000018cef]]
Dockerfileをいじらず、confの中でletsencryptの証明書を指すようにする

なんかうまくいかない、寝よう


2024-06-19
寝て起きてスッキリした頭で再度考える

まず何を目的として何をやろうとしているのか言語化して発信すべきだな
- 冒頭部に書いた

現状の問題
- 僕のサーバ周りの技術力が低くてつまずいている

まず落ち着いてエントリーポイントから順に何が起こっているか確認する
[https://github.com/nishio/polis](https://github.com/nishio/polis)
[[cursor]]で開いた

make PROD startすると何が起こる？


make PROD start を実行すると、以下のことが起こります：
1. PROD ターゲットが実行される:
ENV_FILE が prod.env に設定されます。
TAG が prod.env ファイルから取得されます。
COMPOSE_FILE_ARGS が -f docker-compose.yml に設定されます。
2. start ターゲットが実行される:
echo_vars ターゲットが実行され、現在の ENV_FILE と TAG の値が表示されます。
docker compose コマンドが COMPOSE_FILE_ARGS と ENV_FILE を使用して、すべての Docker コンテナを起動します。
具体的なコマンドの流れは以下の通りです：
make

```
PROD: ## Run in prod mode (e.g. `make PROD start`, etc.) using config in `prod.env`
	$(eval ENV_FILE = prod.env)
	$(eval TAG = $(shell grep -e ^TAG ${ENV_FILE} | awk -F'[=]' '{gsub(/ /,"");print $$2}'))
	$(eval COMPOSE_FILE_ARGS = -f docker-compose.yml)

start: echo_vars ## Start all Docker containers
	docker compose ${COMPOSE_FILE_ARGS} --env-file ${ENV_FILE} up
```

この結果、prod.env ファイルの設定に基づいて Docker コンテナが起動されます。


docker-compose.ymlが実行されるとどうなる？


docker-compose.yml が実行されると、以下のことが起こります：
1. サービスの定義に基づいてコンテナが作成され、起動される:
server, math, postgres, nginx-proxy, file-server の各サービスが定義されており、それぞれのサービスに対応する Docker イメージがビルドまたはプルされます。
各サービスは指定された環境変数、ボリューム、ネットワーク設定に従って起動されます。
2. ネットワークの作成:
polis-net というカスタムネットワークが作成され、すべてのサービスがこのネットワークに接続されます。
3. ボリュームの作成:
backups, postgres, server-logs という名前のボリュームが作成され、対応するサービスにマウントされます。
具体的なサービスの動作は以下の通りです：
server:
./server ディレクトリから Docker イメージをビルドし、prod ターゲットを使用。
server-logs ボリュームにログを保存。
postgres と file-server に依存。
math:
./math ディレクトリから Docker イメージをビルド。
必要な環境変数を設定。
postgres に依存。
postgres:
./server ディレクトリから Dockerfile-db を使用してイメージをビルド。
データベースの環境変数を設定。
backups と postgres ボリュームを使用。
nginx-proxy:
./file-server ディレクトリから nginx.Dockerfile を使用してイメージをビルド。
server に依存。
ポート 80 と 443 をホストに公開。
file-server:
ルートディレクトリから file-server/Dockerfile を使用してイメージをビルド。
必要な環境変数を設定。
これにより、すべてのサービスが連携して動作し、アプリケーション全体が起動されます。

(file-serverの中にnginx-proxy用のファイルがあるのかよ！<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>)


Nginxがテスト用の証明書を使ってしまう問題を解決しようとしている、次はnginx.Dockerfileを読めばいいか？


はい、次に nginx.Dockerfile を読むのは良いアプローチです。nginx.Dockerfile を確認することで、Nginx イメージのビルドプロセスや、どの証明書が使用されているかを理解できます。
特に以下の点に注意して確認してください：
1. 証明書のコピー:
Dockerfile 内で証明書ファイルがどこからコピーされているか。
どのディレクトリに配置されているか。
2. Nginx 設定ファイル:
証明書のパスが Nginx 設定ファイルでどのように指定されているか。
3. ビルドコンテキスト:
ビルドコンテキストに正しい証明書ファイルが含まれているか。
これらの情報を確認することで、テスト用の証明書が使用されてしまう問題の原因を特定し、適切な証明書を使用するように修正できます。


nginx.Dockerfileでは設定ファイルとテスト用の証明書をコピーしている。設定ファイルを適切に編集すれば本番用の証明書を読むと思うがどうか？


はい、Nginx の設定ファイルを適切に編集することで、本番用の証明書を使用するように設定できます。以下の手順で進めると良いでしょう：
1. 本番用の証明書を準備:
本番用の証明書 (cert.pem) と秘密鍵 (key.pem) を適切なディレクトリに配置します。
2. Nginx 設定ファイルの編集:
nginx/nginx-ssl.site.default.conf ファイルを編集し、本番用の証明書と秘密鍵のパスを指定します。
例として、Nginx 設定ファイルの一部を以下のように編集します：
:

```
server {
    listen 443 ssl;
    server_name your_domain.com;

    ssl_certificate /etc/nginx/certs/your_production.cert.pem;
    ssl_certificate_key /etc/nginx/certs/your_production.key.pem;

    # その他の設定
}
```


3. Dockerfile の修正:
本番用の証明書を Docker イメージにコピーするように nginx.Dockerfile を修正します。
:

```
FROM docker.io/nginx:1.21.5-alpine
COPY nginx/nginx-ssl.site.default.conf /etc/nginx/conf.d/default.conf
COPY nginx/certs/your_production.cert.pem /etc/nginx/certs/your_production.cert.pem
COPY nginx/certs/your_production.key.pem /etc/nginx/certs/your_production.key.pem

EXPOSE 80
EXPOSE 443
```

これにより、Nginx は本番用の証明書を使用して起動されるようになります。


あああ！わかった<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
ホストマシンにある証明書をDockerイメージにコピーしないといけないのに、同じマシンの気持ちでパスで指定してる、それだ

 dockerfile

```
COPY /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem /etc/nginx/certs/nhiro-fullchain.pem
COPY /etc/letsencrypt/live/your_domain.com/privkey.pem /etc/nginx/certs/nhiro-privkey.pem
```


 nginx/nginx-ssl.site.default.conf

```
ssl_certificate /etc/nginx/certs/nhiro-fullchain.pem;
ssl_certificate_key /etc/nginx/certs/nhiro-privkey.pem;
```



make PROD startしたけどブラウザでは引き続きテスト用証明書の警告が出ます、なぜ？


make PROD start を実行してもブラウザで引き続きテスト用証明書の警告が出る場合、いくつかの原因が考えられます。以下の点を確認してみてください：
1. Docker イメージのキャッシュ:
Docker イメージがキャッシュされている可能性があります。キャッシュを無効にしてビルドし直してみてください。
cache
2. Nginx 設定のリロード:
Nginx が新しい設定を読み込んでいない可能性があります。Nginx コンテナを再起動してみてください。
proxy
3. 証明書のパスの確認:
nginx.Dockerfile で正しい証明書がコピーされているか確認してください。また、Nginx 設定ファイルで正しいパスが指定されているか確認してください。
4. 証明書の有効性:
本番用の証明書が正しく発行されているか、期限切れになっていないか確認してください。
5. ブラウザのキャッシュ:
ブラウザのキャッシュが原因で古い証明書が表示されている可能性があります。ブラウザのキャッシュをクリアしてみてください。
6. Docker Compose ファイルの確認:
docker-compose.yml ファイルで正しい設定がされているか確認してください。特に、Nginx コンテナの設定を確認してください。
これらの点を確認しても問題が解決しない場合、具体的なエラーメッセージやログを確認することで、問題の原因を特定できるかもしれません。


1や2をmakeでやる手段が用意されてそう


make コマンドを使って Docker イメージのキャッシュを無効にしてビルドし直し、Nginx コンテナを再起動する手段が用意されているかもしれません。以下の Makefile のターゲットを確認してみましょう：
1. キャッシュを無効にしてビルド:
build-no-cache ターゲットが用意されています。これを使って Docker イメージをキャッシュなしでビルドできます。

2. コンテナの再起動:
start-recreate ターゲットが用意されています。これを使ってコンテナを再作成して起動できます。

これらのコマンドを組み合わせて実行することで、問題が解決するかもしれません。

[[CloudWatchで監視]]1


あっ、makeがこけてる
:

```
------
 > [nginx-proxy 5/6] COPY /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem /etc/nginx/certs/nhiro-fullchain.pem:
------
------
 > [nginx-proxy 6/6] COPY /etc/letsencrypt/live/your_domain.com/privkey.pem /etc/nginx/certs/nhiro-privkey.pem:
------
failed to solve: failed to compute cache key: failed to calculate checksum of ref fdb69f4f-67cc-489f-8061-2f3a24921a15::imnifc4l0wil7tzgrsjx1ezl9: "/etc/letsencrypt/live/your_domain.com/privkey.pem": not found
make: *** [Makefile:61: build-no-cache] Error 17
```


ownerがrootだからか？


:

```
27.89 Downloading: com/cnuernber/jarrow/1.000/jarrow-1.000.jar from clojars
27.90 Error building classpath. Could not transfer artifact org.apache.commons:commons-math3:jar:3.6.1 from/to central (https://repo1.maven.org/maven2/): No space left on device
------
failed to solve: process "/bin/sh -c clojure -A:dev -P" did not complete successfully: exit code: 1
make: *** [Makefile:61: build-no-cache] Error 17
```



手順
1. ディスクスペースの確認:
ホストマシンのディスクスペースを確認します。
- `$ df -h`
2. 不要なファイルの削除:
不要なファイルや古い Docker イメージ、コンテナ、ボリュームを削除してディスクスペースを確保します。
:

```
    # 停止中のすべてのコンテナを削除
    docker container prune

    # 使用されていないすべてのイメージを削除
    docker image prune -a

    # 使用されていないすべてのボリュームを削除
    docker volume prune

    # 使用されていないすべてのネットワークを削除
    docker network prune
```


before

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  6.5G  217M  97% /
```


after

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  6.0G  752M  90% /
```

いや、それでもカツカツやん

:

```
------
 > [file-server client-participation 4/6] RUN npm ci --production=false:
1.505 npm warn config production Use `--omit=dev` instead.
47.22 npm warn tar TAR_ENTRY_ERROR ENOSPC: no space left on device, write
47.28 npm notice
47.28 npm notice New minor version of npm available! 10.7.0 -> 10.8.1
47.28 npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.8.1
47.28 npm notice To update run: npm install -g npm@10.8.1
47.28 npm notice
47.29 npm error code ENOSPC
47.29 npm error syscall write
47.29 npm error errno -28
47.29 npm error nospc ENOSPC: no space left on device, write
47.29 npm error nospc There appears to be insufficient space on your system to finish.
47.29 npm error nospc Clear up some disk space and try again.
47.30 
47.30 npm error A complete log of this run can be found in: /root/.npm/_logs/2024-06-19T05_44_05_167Z-debug-0.log
------
------
 > [file-server client-report 6/7] COPY client-report/. .:
------
failed to solve: process "/bin/sh -c npm ci --production=false" did not complete successfully: exit code: 228
make: *** [Makefile:61: build-no-cache] Error 17
```


ダメじゃん

:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  6.4G  359M  95% /
```


:

```
    sudo apt-get clean
    sudo apt-get autoremove
```


:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  6.2G  577M  92% /
```




拡張したい、EC2です


EC2 インスタンスのディスクスペースを拡張するには、以下の手順を実行します。
手順
1. EC2 インスタンスの停止:
まず、EC2 インスタンスを停止します。

2. EBS ボリュームのサイズ変更:
EC2 管理コンソールにログインし、対象のインスタンスにアタッチされている EBS ボリュームを見つけます。
ボリュームを選択し、「アクション」メニューから「ボリュームの変更」を選択します。
新しいサイズを指定して変更を保存します。

3. EC2 インスタンスの起動:
インスタンスを再起動します。

4. ファイルシステムの拡張:
インスタンスに SSH で接続し、ファイルシステムを拡張します。
:

```
    # ルートファイルシステムのデバイス名を確認
    lsblk

    # ルートファイルシステムが /dev/xvda1 であると仮定
    sudo growpart /dev/xvda 1

    # ファイルシステムを拡張
    sudo resize2fs /dev/xvda1
```



> EC2 管理コンソールにログインし、対象のインスタンスにアタッチされている EBS ボリュームを見つけます。
![image](https://gyazo.com/db22e35a7f140bde02961a3653ed375a/thumb/1000)
ふむふむ
![image](https://gyazo.com/8e34baa2baa0825a41c07ba63a211062/thumb/1000)
![image](https://gyazo.com/90a31dd0749d83ae2fa54c2b4ac4a5ff/thumb/1000)
- optimizing (0%)の状態でインスタンスを開始していいのかな

:

```
$ lsblk
NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0      7:0    0 25.2M  1 loop /snap/amazon-ssm-agent/7983
loop1      7:1    0 55.7M  1 loop /snap/core18/2812
loop2      7:2    0 25.2M  1 loop /snap/amazon-ssm-agent/7993
loop3      7:3    0 55.7M  1 loop /snap/core18/2823
loop4      7:4    0 38.7M  1 loop /snap/snapd/21465
loop5      7:5    0 38.8M  1 loop /snap/snapd/21759
xvda     202:0    0   16G  0 disk 
├─xvda1  202:1    0   15G  0 part /
├─xvda14 202:14   0    4M  0 part 
├─xvda15 202:15   0  106M  0 part /boot/efi
└─xvda16 259:0    0  913M  0 part /boot
```


:

```
$ sudo growpart /dev/xvda 1
NOCHANGE: partition 1 is size 31455199. it cannot be grown
```


よくみるとgrowpart相当のことはもうしてあるな

:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        15G  6.2G  8.3G  43% /
```

ファイルシステムも拡張済みか

再ビルド
エラー
あっ
:

```
COPY /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem /etc/nginx/certs/nhiro-fullchain.pem
COPY /etc/letsencrypt/live/your_domain.com/privkey.pem /etc/nginx/certs/nhiro-privkey.pem
```

"your_domain.com"じゃん...


ビルド待ちの間に、インスタンス再起動でIPアドレスが変わったのでDNSを更新しないと
52.91.132.130

![image](https://gyazo.com/d94651674606127524eba837083a2c0e/thumb/1000)
DiskReadとかが取れてないのはエージェントが必要なのかな



nginx-proxy コンテナだけをリビルドするには、以下の手順を実行します。
:

```
# nginx-proxy コンテナを停止
docker compose stop nginx-proxy

# nginx-proxy コンテナを削除
docker compose rm -f nginx-proxy

# nginx-proxy コンテナをビルド
docker compose build nginx-proxy

# nginx-proxy コンテナを再起動
docker compose up -d nginx-proxy
```



:

```
=> ERROR [nginx-proxy 5/6] COPY /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem /etc/nginx/certs/nhiro-fullchain.pem                                                           0.0s
 => ERROR [nginx-proxy 6/6] COPY /etc/letsencrypt/live/polis.nhiro.org/privkey.pem /etc/nginx/certs/nhiro-privkey.pem                                                               0.0s
------
 > [nginx-proxy 5/6] COPY /etc/letsencrypt/live/polis.nhiro.org/fullchain.pem /etc/nginx/certs/nhiro-fullchain.pem:
------
------
 > [nginx-proxy 6/6] COPY /etc/letsencrypt/live/polis.nhiro.org/privkey.pem /etc/nginx/certs/nhiro-privkey.pem:
------
failed to solve: failed to compute cache key: failed to calculate checksum of ref fdb69f4f-67cc-489f-8061-2f3a24921a15::y630wak98lsqz4tftvmxyloof: "/etc/letsencrypt/live/polis.nhiro.org/privkey.pem": not found
make: *** [Makefile:61: build-no-cache] Error 17
```


ん
`$ sudo ls /etc/letsencrypt/live/polis.nhiro.org/privkey.pem`
/etc/letsencrypt/live/polis.nhiro.org/privkey.pem

あるのに？


1. Docker ビルドコンテキストの確認
Dockerfile の COPY コマンドは、ビルドコンテキスト内のファイルを参照します。ビルドコンテキストに /etc/letsencrypt/live/polis.nhiro.org/privkey.pem が含まれていない可能性があります。
方法 1: Docker ビルドコンテキストに証明書をコピー
1. 証明書ファイルをプロジェクトディレクトリにコピー
証明書ファイルをプロジェクトディレクトリにコピーします。


コピーだとcertbotが更新した時に古い方を使い続けてしまうからln -sしたらどうかな


ln -s を使ってシンボリックリンクを作成するのは良いアイデアです。これにより、Certbot が証明書を更新した際に自動的に新しい証明書が使用されるようになります。


こうした
:

```
COPY nginx/cert/nhiro-fullchain.pem  /etc/nginx/certs/nhiro-fullchain.pem
COPY nginx/cert/nhiro-privkey.pem /etc/nginx/certs/nhiro-privkey.pem
```



:

```
 => ERROR [nginx-proxy 5/6] COPY nginx/cert/nhiro-fullchain.pem  /etc/nginx/certs/nhiro-fullchain.pem                                                                               0.0s
 => ERROR [nginx-proxy 6/6] COPY nginx/cert/nhiro-privkey.pem /etc/nginx/certs/nhiro-privkey.pem                                                                                    0.0s
------
 > [nginx-proxy 5/6] COPY nginx/cert/nhiro-fullchain.pem  /etc/nginx/certs/nhiro-fullchain.pem:
------
------
 > [nginx-proxy 6/6] COPY nginx/cert/nhiro-privkey.pem /etc/nginx/certs/nhiro-privkey.pem:
------
failed to solve: failed to compute cache key: failed to calculate checksum of ref fdb69f4f-67cc-489f-8061-2f3a24921a15::m8mkj6rtbq8r4rggxmzjlbgkw: "/nginx/cert/nhiro-privkey.pem": not found
make: *** [Makefile:61: build-no-cache] Error 17
```

えー
- "/nginx/cert/nhiro-privkey.pem"
- この文脈で/nginxにアクセスする理由が謎
- ln -sしないでcpすることにした
    - 前回はcpしたはず
    - 証明書の更新方法は後で考える

これ「なんで/nginx？」という方に気を取られてたが`cert`ではなく`certs`だな

やっと直った！！

[[CloudWatchで監視]]2


証明書のエラーは解消されたが"polis.nhiro.org で接続が拒否されました。"になる

:

```
$ docker logs polis-dev-nginx-proxy-1
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: /etc/nginx/conf.d/default.conf differs from the packaged version
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/06/19 08:48:42 [emerg] 1#1: cannot load certificate key "/etc/nginx/certs/nhiro-privkey.pem": PEM_read_bio_PrivateKey() failed (SSL: error:0909006C:PEM routines:get_name:no start line:Expecting: ANY PRIVATE KEY)
nginx: [emerg] cannot load certificate key "/etc/nginx/certs/nhiro-privkey.pem": PEM_read_bio_PrivateKey() failed (SSL: error:0909006C:PEM routines:get_name:no start line:Expecting: ANY PRIVATE KEY)
```


もう一度落ち着いてdockerfileをみる
:

```
FROM docker.io/nginx:1.21.5-alpine

COPY nginx/nginx-ssl.site.default.conf /etc/nginx/conf.d/default.conf

# We only use these in testing.
COPY nginx/certs/snakeoil.cert.pem /etc/nginx/certs/snakeoil.cert.pem
COPY nginx/certs/snakeoil.key.pem  /etc/nginx/certs/snakeoil.key.pem

COPY nginx/certs/nhiro-fullchain.pem  /etc/nginx/certs/nhiro-fullchain.pem
COPY nginx/certs/nhiro-privkey.pem /etc/nginx/certs/nhiro-privkey.pem

EXPOSE 80
EXPOSE 443
```


間違ってはいない


1. 証明書ファイルの内容を確認
nhiro-privkey.pem ファイルの内容が正しい形式であることを確認します。ファイルの先頭が -----BEGIN PRIVATE KEY----- または -----BEGIN RSA PRIVATE KEY----- で始まり、末尾が -----END PRIVATE KEY----- または -----END RSA PRIVATE KEY----- で終わっていることを確認します。

3. 証明書ファイルの権限が正しいことを確認します。ファイルの読み取り権限が Nginx に与えられていることを確認します。
sudo chmod 644 /path/to/your/project/nginx/cert/nhiro-privkey.pem

ああ〜600だ〜〜〜<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

やっと動いた！！
![image](https://gyazo.com/64e5abe391390d648c294818eb5a1c39/thumb/1000)
unauthorized domainになるのは既知

.env

```
# If you are running polis on a custom domain, set both API_PROD_HOSTNAME and DOMAIN_OVERRIDE
# to the same value. In the future these will be combined into one setting.
API_PROD_HOSTNAME=pol.is
DOMAIN_OVERRIDE=
```

これを
.env

```
API_PROD_HOSTNAME=polis.nhiro.org
DOMAIN_OVERRIDE=polis.nhiro.org
```

こうだな

![image](https://gyazo.com/70cec473da1d47fbb8ef80b2d25a01f3/thumb/1000)
`https://polis.nhiro.org`なのでは？

:

```
info: not whitelisted {"headers":{"accept":"application/json, text/javascript, */*; q=0.01","accept-encoding":"gzip, deflate, br, zstd","accept-language":"ja,en-US;q=0.9,en;q=0.8,zh;q=0.7,zh-CN;q=0.6,zh-HK;q=0.5,zh-TW;q=0.4","cache-control":"max-age=0","connection":"close","content-length":"97","content-type":"application/json; charset=UTF-8","host":"polis.nhiro.org","origin":"https://polis.nhiro.org","priority":"u=1, i","referer":"https://polis.nhiro.org/createuser","sec-ch-ua":"\"Google Chrome\";v=\"125\", \"Chromium\";v=\"125\", \"Not.A/Brand\";v=\"24\"","sec-ch-ua-mobile":"?0","sec-ch-ua-platform":"\"macOS\"","sec-fetch-dest":"empty","sec-fetch-mode":"cors","sec-fetch-site":"same-origin","user-agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36","x-forwarded-proto":"https","x-requested-with":"XMLHttpRequest"},"path":"/api/v3/auth/new","service":"polis-api-server","timestamp":"2024-06-19 09:34:40 +00:00"}
POST /api/v3/auth/new 500 4.790 ms - 45
unauthorized domain: https://polis.nhiro.org
```


はてな
> できた --- [[EC2でPolis#646d8611aff09e0000bf04d0]]
- どうやってできたんだよ！

前回.envとprod.envがあるのに混乱した記憶があり、今回はずっとprod.envでやってたが
:

```
# Optionally give the server container a distinct env_file. Useful for CI tests.
SERVER_ENV_FILE=.env
```

もしかしてprod.envにこれをデフォルト値のまま残してるのがまずいのか

むしろdomainOverrideがnullなんだが`make PROD start`してても`prod.env`が読まれてないのでは
:

```
$ make PROD start
make: 'PROD' is up to date.
ENV_FILE=prod.env
TAG=dev
docker compose -f docker-compose.yml --env-file prod.env up
```

そんなことないな

2024-06-21
prod.envは読んでるはずなのにdomainOverrideがnullなのが不自然なのでそこを調べる

[[CloudWatchで監視]]

[[Polis テスト用の質問リストを作る]]

feedback
- ホスト選択肢: fly.io
- 証明書選択肢: AWS Certificate manager
    - > ACM で作ったものを ALB につなげてそこで SSL 終端し、サーバ側は HTTP だけ返すようにする
- 監視系は Cloudwatch だと メモリの監視がなかったりカスタマイズが必要なので、 datadog などの SaaS を使うのがさっとできて楽かも

2024-06-22
全然時間取れてないw

before
`SERVER_ENV_FILE=`
after
`SERVER_ENV_FILE=prod.env`
`$ make build-no-cahce`

:

```
services:
  server:
    env_file:
      - ${SERVER_ENV_FILE:-.env}
```

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
- SERVER_ENV_FILEは.envファイルのパスを指定する環境変数です。この環境変数の値によって、サービスの設定や動作が変わることがあります。以下に詳細を示します。
    - 指定されていない場合（デフォルト値 .env）:
        - サーバーはプロジェクトのルートディレクトリにある .env ファイルを使用します。
            - えーー<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
                - こんがらがりすぎでは...
    - 特定のファイルが指定されている場合:
        - 例えば、SERVER_ENV_FILE=.env.production と指定されている場合、サーバーは .env.production ファイルを使用します。


:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        15G   15G  253M  99% /
```

あったらあっただけ使うのか？w
:

```
    # 停止中のすべてのコンテナを削除
    docker container prune
    # 使用されていないすべてのイメージを削除
    docker image prune -a
    # 使用されていないすべてのボリュームを削除
    docker volume prune
    # 使用されていないすべてのネットワークを削除
    docker network prune
```

:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        15G   14G  627M  96% /
```

なにが嵩張ってるんだ？
:

```
$ sudo du -h --max-depth=1 /
12G     /var
```

:

```
/var$ sudo du -h --max-depth=1 .
12G     ./lib
```

:

```
/var/lib$ sudo du -h --max-depth=1 .
11G     ./docker
```

:

```
$ docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - unused build cache

Are you sure you want to continue? [y/N] y
Deleted build cache objects:
...
Total reclaimed space: 7.928GB
```

これか
:

```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        15G  3.5G   12G  24% /
```

build cacheを消すべきだと気づいていればディスクの拡張はいらなかったかもな

戻る
`$ make build-no-cahce`
`$ make PROD start`
![image](https://gyazo.com/80b314a50c1df680e3a7533ebb239204/thumb/1000)
できた！！

