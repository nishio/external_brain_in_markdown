---
title: "YouTubeのコメント/トランスクリプト/ライブチャット取得"
---

コードはここにおいた: [https://github.com/nishio/from_youtube](https://github.com/nishio/from_youtube)
- YouTubeライブにリアルタイムでついてるコメントは「コメント」ではなく「ライブチャット」と呼ぶのが正しい
- ライブチャットの取得にAPIキーは必要なかった
- 2024-11-15時点でコメント/トランスクリプト/ライブチャットの取得ができているがYouTube側の更新で動かなくなる可能性はありそう

---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>YouTubeのコメントをPythonでダウンロードしたい

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>YouTubeのコメントをPythonでダウンロードするには、google-authやgoogle-auth-oauthlib、そしてgoogle-auth-httplib2などのライブラリを用いてYouTube Data API v3を利用するのが一般的です。以下がその手順の概要です。

APIキーを取得
- Google Cloud Consoleで新規プロジェクトを作成し、YouTube Data API v3を有効化した後、APIキーを取得します。
    - リストから探したけど見つけられなかった、検索したら見つかった<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - ![image](https://gyazo.com/c7e1beefcfdddc725b20506736815042/thumb/1000)


Pythonパッケージのインストール
- 以下のようにパッケージをインストールします。
- $pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client

コードの作成
取得したAPIキーを使用してYouTubeの動画からコメントを取得します。以下にサンプルコードを示します。
...
- 動いたけど欲しかったものは「コメント」ではなく「ライブチャット」だった
