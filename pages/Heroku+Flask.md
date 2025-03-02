
2020-09-15: 機械学習や自然言語処理なんかのAPIサーバをherokuで動かしたい時のための作業メモ
- 2021-01-18: [[Herokuで自然言語処理]]
- 2021-10-14: [[FastAPI]]という選択肢もあるので要検討(今回はFastAPIをちょっと試してからFlaskに戻った)

まず最小限のサーバを作ってローカルで動かす
- `$ python3 -m venv venv`
- `$ source venv/bin/activate`
- create "server/__init__.py" and write minimal server
python

```
from flask import Flask

app = Flask(__name__)

def create_app():
    return app

@app.route('/')
def root():
    return "OK"
```

    - 最小限のサーバ実装
    - 昔の記憶なのか `if __name__ == "__main__"`でapp.runしちゃう癖があったのだがFlaskの公式チュートリアルでも、もうそれはやってない
        - 環境変数で起動すべきモジュールを指定し、flask runで起動するスタイル
            - [heroku側の解説](https://devcenter.heroku.com/articles/flask-memcache)でもそうしてる
            - 環境変数を設定するのが面倒に思うかもしれないが、dotenvを使えば良い
            - 公式解説では[[Flask Blueprint]]を使ってるけどそれは最小限の時には必要ないと判断した
        - create_appは後でgunicornから呼ぶのに使う
- `$ python server/__init__.py`
    - `ModuleNotFoundError: No module named 'flask'`
        - `$ pip install --upgrade pip`
        - `$ pip install flask`
    - OK
- `$ flask run`
    - 環境変数が設定されてないのでNG
    - > Error: Could not locate a Flask application. You did not provide the "FLASK_APP" environment variable, and a "wsgi.py" or "app.py" module was not found in the current directory.
- create ".env" file
    - `$ code .env`
:

```
FLASK_APP=server
FLASK_ENV=development
```

- `$ pip install python-dotenv`
- `$ flask run`
    - OK
    - ブラウザで [http://127.0.0.1:5000/](http://127.0.0.1:5000/) を見ればOKと表示される

herokuにデプロイする
- `$ git init`
- create ".gitignore"
:

```
venv/
.env

*.pyc
__pycache__/
```

    - .env ignoreしちゃうの？
        - ignoreしなければ後で行う $ heroku config:set FLASK_APP=server が不要になる
        - これは.envに公開してはいけないAPIキーなどを置いて公開リポジトリにpushしてしまうよくある事故を避けるため
- `$ git add .`
- `$ git commit -m 'minimal Flask server'`

- `$ heroku create foo-server`
    - これはローカルのコンソールからappをcreateしているが、既にブラウザなどから使ってある場合はブラウザに解説が出ている通り下記で良い
        - `$ heroku git:remote -a foo-server`
- `$ git remote`
    - >  heroku
- ここでpushしてみる
    - `$ git push --set-upstream heroku master`
    - pushはできるがビルドで失敗する
- `$ pip install gunicorn`
- `$ pip freeze > requirements.txt`
- create "Procfile"
:

```
web: gunicorn server:"create_app()"
```

    - name "server" points the module on "./server"
- `$ heroku config:set FLASK_APP=server`
- add and commit
- `$ git push heroku master`
    - ビルドに成功するのを確認する
- `$ heroku open`
    - ブラウザで開いてOKと表示されるのを確認する

必要なAPIを実装する
- pushしたときのビルドログと、アクセスしたときのエラーログを見る
    - `$ heroku logs --tail`
    - 必要なファイルを含め忘れててアクセス時に実行時エラーになってたり
    - ビルド時にエラーになってたり: [mecabがno such file or directory: /usr/local/etc/mecabrc](https://medium.com/@jiraffestaff/mecabrc-%E3%81%8C%E8%A6%8B%E3%81%A4%E3%81%8B%E3%82%89%E3%81%AA%E3%81%84%E3%81%A8%E3%81%84%E3%81%86%E3%82%A8%E3%83%A9%E3%83%BC-b3e278e9ed07)
- `By default, a route only answers to GET requests.`[doc](https://flask.palletsprojects.com/en/2.0.x/quickstart/#http-methods)
    - `@app.route('/', methods=['GET', 'POST'])`
- JSON
    - `property json: Optional[Any]` [doc: Incoming Request Data](https://flask.palletsprojects.com/en/2.0.x/api/#incoming-request-data)
        - > The parsed JSON data if mimetype indicates JSON (application/json, see is_json).
- 他のオリジンから呼ぶなら: [[Flask-CORS]]が必要

"No web processes running"
- Procfileのファイル名をtypoしてた
- ビルド自体は通ってしまう…


----old memo
[[Heroku+Flask 2019-6-07 memo]]