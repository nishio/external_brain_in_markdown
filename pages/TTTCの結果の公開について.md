---
title: "TTTCの結果の公開について"
---

Github Pages
- [GitHub Pages | Websites for you and your projects, hosted directly from your GitHub repository. Just edit, push, and your changes are live.](https://pages.github.com/)
- リポジトリが公開でも良いなら楽、非公開でいいなら課金が必要
- デフォルトだとJekyllで書かれていると判断するので`.nojekyll`を置いてJekyllをオフにする

Netlify
- [Scale & Ship Faster with a Composable Web Architecture | Netlify](https://www.netlify.com/)
- 非公開で共有する方法の一つ
- [東京都知事選2024におけるTalk to the Cityの活用ノウハウ｜NISHIO Hirokazu](https://note.com/nishiohirokazu/n/n0661204bda5b)
    - > 内部向けプレビューサーバを開発してNetlifyでホストしました。Netlifyでもprivateリポジトリからの継続的デプロイは有償機能なのですが、1ヶ月の試用期間があったので選挙期間中は無償で実行できました。


Amazon S3
- [Amazon S3](https://aws.amazon.com/jp/pm/serv-s3/)
- 非公開で共有する方法の一つ
- `http://<bucketname>.s3-website-us-east-1.amazonaws.com/`みたいなURLになるのが難点
- [[社内TTTC]]で使った
- 結果は社員だけに公開する想定で、一般には公開しない
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>S3にindex.htmlをアップロードした後、静的ウェブサイトとして公開するためには以下の手順を実行します。
    - バケットの静的ウェブサイトホスティングを有効にする:
        - S3コンソールで、対象のバケットに移動します。
        - 「プロパティ」タブを開き、「静的ウェブサイトホスティング」という項目を見つけて有効化します。
        - インデックスドキュメントにindex.htmlを指定します。
    - パーミッションの設定:
        - index.htmlがパブリックにアクセス可能である必要があります。
        - S3コンソールの「アクセス権限」タブで、バケットポリシーを設定し、パブリックアクセスを許可します。
        - 例として、以下のようなポリシーを追加します（your-bucket-nameを実際のバケット名に置き換えてください）：
json

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

    - 公開URLの確認:
        - 「静的ウェブサイトホスティング」を有効にすると、指定されたURLが表示されます。
        - このURLを使ってindex.htmlにアクセスできます。
- 以上で、S3上でホストしたHTMLサイトがパブリックにアクセス可能になります。

[[Talk to the City]]