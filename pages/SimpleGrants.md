---
title: "SimpleGrants"
---

[[フィアット]]で[[Quadratic Funding]]するツール
[https://github.com/supermodularxyz/simplegrants](https://github.com/supermodularxyz/simplegrants)




手元で動かそうと試行錯誤したログ

これを見る
- [/tkgshn/Simple Grantをローカルでビルドしてみる](https://scrapbox.io/tkgshn/Simple Grantをローカルでビルドしてみる)

### BackendのREADMEを見る
> You have to use Node version >= 17.5!
`% node -v`
> v21.2.0


> all you need to do is to change the payment provider in [`provider.service.ts`](./src/provider/provider.service.ts#L15) to the provider you want to use.

ts

```typescript
export class ProviderService {
  constructor(private readonly prisma: PrismaService) {
    this.paymentProvider = new StripeProvider({
      prisma,
      secret: process.env.PAYMENT_KEY,
      country: 'US',
    });
  }
```

Stripeを使うためにはこの設定をする必要があるがとりあえず無視


`% npm install`
:

```
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'next-auth@4.18.8',
npm WARN EBADENGINE   required: { node: '^12.19.0 || ^14.15.0 || ^16.13.0 || ^18.12.0' },
npm WARN EBADENGINE   current: { node: 'v21.2.0', npm: '10.2.3' }
npm WARN EBADENGINE }
```

Dockerを立ち上げるのになんでnpmでnext-authをインストールするんだ？
とりあえず無視


`$ npm run docker:up`
![image](https://gyazo.com/1712cf6178e7bcb3c8015bd663cafb61/thumb/1000)
![image](https://gyazo.com/718e59e326adc25aedcb928a8805dd84/thumb/1000)

コンテナは立ち上がった


## frontend
`$ npm install -g yarn`
`$ yarn install`
`$ cp .env.example .env.local`
`$ yarn dev -p 3001`

とりあえず起動はした
![image](https://gyazo.com/3c1a537de9e0536dc658aa1ea40b614f/thumb/1000)
API key requiredとは何か
- `NEXT_PUBLIC_FINGERPRINT_KEY`に何を入れるのか調べる
- [The device intelligence platform | Fingerprint](https://fingerprint.com/)
    - これか
    - 解決した✅
    - なぜ入れる？QFだから複数アカウント作られたくない的なこと？

この辺のどこかで本家からcloneしたのを消して
[https://github.com/Naokiakazawa/simplegrants/tree/verification](https://github.com/Naokiakazawa/simplegrants/tree/verification)
からやることにした(akazawaさんが隣の席にいたのでその方が効率的と判断)

### Sign upを動くようにする
.envのサンプルにはないけど[code](https://github.com/supermodularxyz/simplegrants/blob/main/frontend/pages/api/auth/%5B...nextauth%5D.ts)で`process.env`から設定を読んでる。
- GOOGLE_CLIENT_ID / GOOGLE_CLIENT_SECRET だけ設定することにした
- [[OAuth 2.0]]

[Setting up OAuth 2.0 - Google Cloud Platform Console Help](https://support.google.com/cloud/answer/6158849?hl=en)
雑に設定して`GOOGLE_CLIENT_ID`と`GOOGLE_CLIENT_SECRET`を入れたが`'"ikm" must be at least one byte in length'`になってしまった
- 何をどう設定しておく必要があったのか
- あー`NEXTAUTH_SECRET`か
    - [next.js - "ikm" must be at least one byte in length - Stack Overflow](https://stackoverflow.com/questions/72518497/ikm-must-be-at-least-one-byte-in-length)
- どうやって取得？
- randomでいいらしい
    - `$ openssl rand -base64 32`
    - これでもいい: [https://generate-secret.vercel.app/32](https://generate-secret.vercel.app/32)

### redirect_uri_mismatch
ここまでできた
- ![image](https://gyazo.com/924e55f3366ad5eeaaf2f4a79d1251af/thumb/1000)
- redirect urlを設定する必要があるのだな
- サンプルもらった
    - ![image](https://gyazo.com/32e64cd5009613f4139f37260c5e9cc0/thumb/1000)

### frontendもdockerで動かす必要がある
READMEにそんなことは一言も書いてない
- `yarn install`して`yarn dev -p 3001`しろと書いてるのでいかにも普通に動きそう
- しかしfrontendの.envでDATABASE_CONTAINERを参照しており(なぜ？[[Prisma]]は何をしてる？)
.env.local

```
# Prisma ENV
DATABASE_URL="postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${DATABASE_CONTAINER}:5432/${POSTGRES_USER}?schema=public&connect_timeout=300"
```

- そのためfrontendからコンテナの名前でアクセスが通る必要がある
    - docker-compose.yamlなどで`networks: simplegrants`的な設定をしている、これが大事、多分
    - frontendを起動した時に「Network Error」とトースターが出るのはこれが原因、多分

project rootでdocker composeする
- `$ docker compose -f docker-compose.dev.yml up --build`

その後root/backendでDB初期化
- `$ cd backend`
- `$ yarn setup`
:

```
All migrations have been successfully applied.
Environment variables loaded from .env
Running seed command `ts-node prisma/seed` ...

An error occurred while running the seed command:
Error: Command failed with ENOENT: ts-node prisma/seed
spawn ts-node ENOENT
```

- こんなエラーが出るのだけど？？？

### redirect_uri_mismatchの続き
- 一度`http://`を`https://`にするミスをした
- 一歩進んだ
    - ![image](https://gyazo.com/b19792cb28d5c9e35b3f88dd697b89eb/thumb/1000)

    - Publishing status: In productionにした

### no PostgreSQL user name specified in startup packet
- ログインダイアログはエラーにならずに完了したが
    - `2024-01-31 02:44:34.623 UTC [93] FATAL:  no PostgreSQL user name specified in startup packet`
    - ユーザデータを書き込もうとして死んでる...
- 原因
    - `$ docker compose -f docker-compose.dev.yml up --build`
    - ここでは`docker-compose.dev.yml`を使ってるのだから.env.productionではなく.env.localが読まれる
    - FIX: .env.productionに書いてたPOSTGRES_USER/POSTGRES_PASSWORDを.env.localにも書く


docker composeからやり直したらできた！
- ![image](https://gyazo.com/3f920c6bf0f66c440a564cfa0fe63fd3/thumb/1000)
    - サンプルデータが入ってないぞ？
- localhost:3000/apiで[[Swagger]]が出るのは確認した
- まだやってないこと: [[Stripe]]の設定
