
- [[2019未踏ジュニア]]で[[Mattermost]]が導入された
- [[tokoroten]]が[[Vein]]を接続したいと言い出して、どうせならみんなHackableな方がいいよねとなった
- というわけでみんな色々繋げれるようになったから僕も[[チャットボット]]を作ってみた

- Incoming Webhookを設定する
    - 設定したら[[curl]]でリクエストを投げてみる
    - `$ curl -i -X POST -d 'payload={"text": "日本語!"}' https://mattermost....`
    - 正しく設定できていればこんな感じになる
        - ![image](https://gyazo.com/e90b122c87fd934b6155d1179ab77345/thumb/1000)
        - プロフィール画像の設定がファイルアップロードではなく画像URLの指定だった

- Slash Commandを設定する
    - チャットボット自体には使わないかもだけど一歩一歩進むためにこれをやる
    - 何がおきているかわかりやすくするために手元のサーバでやる
    - `$ python3 -m http.server`
        - ローカルの8000番ポートでHTTPサーバを立てた
        - ディレクトリ内のファイルが晒されるので見られて困るもののないところでやること
    - `$ ngrok http 8000`
        - ローカルの8000番ポートへ[[ngrok]]でトンネリング
        - ブラウザで `http://***.ngrok.io/` にアクセスしてディレクトリ内が見えることを確認
    - スラッシュコマンドの設定
        - リクエストURL: `http://***.ngrok.io/`
        - リクエストメソッド: GET
    - これでスラッシュコマンドを実行するとサーバにこんなリクエストが届くのが見える
        - GET /?channel_id=***&channel_name=z-botplayground&command=%2Fnisbot&response_url=***&team_domain=***&team_id=***&text=&token=***&user_id=***&user_name=nishio
    - `http.server`はこのリクエストに対して、パラメータを無視してディレクトリ内のファイルの一覧表示のHTMLを返す
    - そのHTMLがMattermost上に表示される
        - ![image](https://gyazo.com/eaf77ef21c4891ea4e481088d7c9a98a/thumb/1000)
    - これで手元のサーバとMattermostが相互にやり取りできることが確認された
    - なおリクエストメソッドをPOSTにするとMattermost上に
        - `トリガー'nisbot'によるコマンドは501 Unsupported method ('POST')状態を返しました`
        - とエラーメッセージが表示される。`http.server`がPOSTに対して501を返すという理由

- Outgoing Webhookを設定する
    - 微妙な落とし穴にはまった:
        - [[Mattermostでスラッシュコマンドと同一のウェイクワードではOutgoing Webhookが起動されない]]
        - `/nisbot`と`nisbot foo`の両方を同時に使うことはできない
        - スラッシュコマンドの側を適当に変更しておく
    - POSTメソッドのリクエストを扱うことのできるサーバを用意する
        - たとえばFlaskを使う
            - [Welcome | Flask (A Python Microframework)](http://flask.pocoo.org/)
        - POSTの受け取り方はここに書いてある
            - [HTTP Methods](http://flask.pocoo.org/docs/1.0/quickstart/#http-methods)
            - 「GETではなく、POSTを受け取る」と記述する
            - これを間違えるとngrokが"405 METHOD NOT ALLOWED"と表示する
        - Mattermostに返事をどう返せば良いかはこれの10に書いてある
            - [Outgoing Webhooks — Mattermost 5.11 documentation](https://docs.mattermost.com/developer/webhooks-outgoing.html)
        - まとめると以下のようなコードになる
python

```
from flask import Flask
import json
app = Flask(__name__)

@app.route("/", methods=["POST"])
def hello():
    return json.dumps(dict(text="hello"))
```

        - `$ FLASK_APP=server.py flask run --port 8000`
            - サーバを起動した
            - ポート8000を指定しているのはhttp.serverに揃えることでngrokを起動し直すのを避けただけ
        - これで話しかけるとhelloと返事してくるようになった
            - ![image](https://gyazo.com/eb4d211c9ee896d8505666b6b7d02562/thumb/1000)

    - 毎回固定文字列の返事では面白くないのでとりあえずパラメータを扱いたい
        - パラメータがどういう名前で渡されるかはこれの8に書いてある
            - [Outgoing Webhooks — Mattermost 5.11 documentation](https://docs.mattermost.com/developer/webhooks-outgoing.html)
python

```
from flask import Flask, request
import json
app = Flask(__name__)

@app.route("/", methods=["POST"])
def hello():
    username = request.form["user_name"]
    text = request.form["text"]
    reply = f"{username}が「{text}」と入力した"
    return json.dumps(dict(text=reply))
```

        - ![image](https://gyazo.com/3f673f2cac3dc5767099cd698a3d35c7/thumb/1000)
        - 作成過程の失敗メモ
            - `from flask import Flask, request`のrequestを忘れて500 Internal Server Errorになった
            - user_nameとすべきところをusernameにすると400 Bad Requestになる
            - コンテントタイプをデフォルトのurlencodedからjsonに変更してても400になる
                - ![image](https://gyazo.com/b77eb98b3c5771f95a8ee21a95ae25e2/thumb/1000)

今回は手元のサーバでbotをつくるところまでをやった
個人的には次はAWS Lambdaを試したいと思っている
- [Mattermostの「褒めbot」をLambdaとPythonで作ってみた - Qiita](https://qiita.com/t15/items/5cae2fc9916363858f6c)
あと、トリガーワードなしで起動するためには
- [OAuth 2.0 Applications — Mattermost 5.11 documentation](https://docs.mattermost.com/developer/oauth-2-0-applications.html)
- とかかなぁ？(まだしっかり読んでない)
- Slackで全メッセージ受信するBOTを作ってる人はいる
    - [Slack で自動返信するサーバレスBOTを作りました - Qiita](https://qiita.com/saitotak/items/822bf2dce7e3baa25ae0)

- PythonからIncoming WebHookを叩いてチャットボットに喋らせる
    - `requests.post(url, json=dict(text="rebooting server..."))`
- 調子に乗ってFORTHを雑に実装して接続した
![image](https://gyazo.com/972ff7262e28caf82ab5d2dc371095a1/thumb/1000)

