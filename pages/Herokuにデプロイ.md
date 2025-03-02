---
title: "Herokuにデプロイ"
---

- [[Heroku]]にアカウントを作る
- 指示に従いCLIをインストール
- アプリを作成
- `$ heroku login`
- `$ heroku create`

- `$ heroku git:remote -a <アプリ名>`
- `$ git add .`
- `$ git commit -am "make it better"`
- `$ git push heroku master`
    - 色々向こう側で起こる

- `$ heroku run python tweet.py`
    - 動作確認

- スケジューラ登録
    - の前にクレジットカードを登録しておかないといけない
        - Verify now at [https://heroku.com/verify](https://heroku.com/verify)
    - `$ heroku addons:create scheduler:standard`
    - `$ heroku addons:open scheduler`
    - ブラウザが立ち上がる
    - 間隔の選択肢少ないぞ
        - ![image](https://gyazo.com/69fe020405cc736c2a2ed8362caebd0d/thumb/1000)
- エラーログを見る
    - heroku logs --tail --app <app-name>
