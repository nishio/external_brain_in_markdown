
ローカルで実験していた自然言語処理のアルゴリズムをHeroku上でAPIサーバにする過程のメモ
(Herokuでやるのが適切かどうかの考察はしてない → [[APIサーバの置き場所考察]])

- 前に似たことをやった時のメモ[[Heroku+Flask]]を参考にする
    - 新しい作業ディレクトリを作る
        - 既存のリポジトリを使うかとか考えたこともあったけども、複雑なことをしてトラブルが起きた時に原因究明に時間がかかって不毛なのでなるべくシンプルにする
        - `$ mkdir regroup-split-server`
        - `$ cd regroup-split-server `
    - 仮想環境を作ってVSCode上で作業する
        - `$ python3 -m venv venv`
        - `$ code .`
        - View -> Terminal
        - `$ source venv/bin/activate`
    - Flaskで最小限のサーバを作る
        - `$ mkdir server`
        - `$ code server/__init__.py`
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

        - `$ pip install --upgrade pip`
        - `$ pip install flask`
        - 環境変数の設定をファイルで行うようにする
            - `$ code .env`
.env

```
FLASK_APP=server
FLASK_ENV=development
```

            - `$ pip install python-dotenv`
        - `$ flask run`
            - 問題なく実行されることと [http://127.0.0.1:5000/](http://127.0.0.1:5000/) を開いてOKが出ることを確認する
        - `$ git init`
        - `$ code .gitignore`
.gitignore

```
venv/     
*.pyc
__pycache__/
```

            - `$ git commit -m 'minimal Flask server'`
                - 実際はVSCodeのSource ControlタブでCmd+Enterしてる
    - [[gunicorn]]を加えてデプロイする
        - これは[[FlaskのHTTPS化]]も兼ねていて、現代のAPIサーバとしてはHTTPだけってわけにもいかないと思うので最小構成に含めてる
        - `$ pip install gunicorn`
        - `$ pip freeze > requirements.txt`
        - `$ code Procfile`
Procfile

```
web: gunicorn server:"create_app()"
```

        - `$ heroku create regroup-split-server`
        - `$ git commit -m "add gunicorn"`
        - `$ git push --set-upstream heroku master`
            - ビルドログが出る。エラーになってないことを確認する
        - `$ heroku open`
            - デプロイされたものをブラウザで開く。OKが表示されてるのを確認する

- このデプロイ用のリポジトリと、ローカルでの研究開発用のリポジトリをどうするかはまだどうするのがスッキリするかわかってない
    - 状況によっては切り離したくなると思うが、どう切り離したいか明確になるまでは一体でやろうと思っている
        - リポジトリを分けた上でハードリンクでつないだこともあったが、良くないと思う
        - git submoduleかpipで繋ぐのがよさそう
            - [Resolving Application Dependencies with Git Submodules | Heroku Dev Center](https://devcenter.heroku.com/articles/git-submodules)
            - [[自分用pip]]

    - 将来切り離しやすいようにフォルダはわけておく
        - `$ mkdir server/regroup_split`
    - 必要そうなファイルをコピー
deploy.sh

```
cp rich_tokenizer.py ../regroup-split-server/server/regroup_split/
cp regroup_split.py ../regroup-split-server/server/regroup_split/
cp TAIL_TOKENS_TO_REMOVE.txt ../regroup-split-server/server/regroup_split/
cp HEAD_TOKENS_TO_REMOVE.txt ../regroup-split-server/server/regroup_split/
cp test/simplelines1.txt ../regroup-split-server/server/regroup_split/test
cp test/regression_test.json ../regroup-split-server/server/regroup_split/test
```


    - 単体テストを走らせて、エラーが出ないから確認する
        - `ModuleNotFoundError: No module named 'MeCab'`
            - $ pip install mecab
                - これをしてはいけない see [[mecab on heroku]]
            - `$ pip install mecab-python3==0.996.5`

    - 単体テストが通ったらそのテストをserver/__init__.pyから呼び出す
        - flask runしてローカルの開発サーバでテストが動くか確認する
        - デプロイした後よりローカルの開発サーバの方がエラーメッセージが読みやすいから
        - よくある修正
            - 相対インポート `from .foo import bar`
                - 普段スクリプトとして実行して実験してるのだけど、サーバからインポートされてモジュールとして実行されるようになるのでインポートの振る舞いが変わる
                - 普段から[[IPythonで%run -m]]するのが良いのかもな
            - データファイルのパス
                - 実行時のカレントディレクトリに依存した書き方をしてるとここでこける
                    - `DIR = os.path.dirname(__file__)`を使う

- ローカルで動くようになったらherokuにpush
    - `$ pip freeze > requirements.txt`
        - addとcommitも忘れないように
        - installした時点でやっとくべきだったか
    - `$ git push`
        - ビルドエラー [[mecab on heroku]]
    - ビルド成功後、heroku openして500エラー
        - 実行時のログを見る
            - `$ heroku logs --tail`
        - `TypeError: 'dict_keys' object is not reversible`
            - herokuのPythonはデフォルトでは3.6
            - > By default, newly created Python apps use the python-3.6.12 runtime. --- [Heroku Python Support | Heroku Dev Center](https://devcenter.heroku.com/articles/python-support)
        - 実行バージョンを手元のものと揃える
            - `$ echo python-3.8.7 > runtime.txt`
    - heroku上でもテストケースが動くようになった

- 今まで端末で実行し、標準出力で結果を観察してた実験スクリプトに、サーバから値を渡された、処理した値を返すためのインターフェイスをつける
    - 今回のケースだと文字列を受け取ってトークン列のリストを返す感じ
    - この時、リッチなオブジェクトを返すのか、jsonでシリアライズ可能なものを返すのが
        - これ単体では用途次第って感じ
        - jsonでシリアライズ可能にする処理ってどこでも求められることだと思うからライブラリの側に入ってるのがいいかな
        - 適切なシリアライズは内部構造が変わると変化しうるし
python

```
def process_single_line(line):
    tokens = tokenize(line)
    calc_split_priority(tokens)
    return dict(
        tokens=concat_tokens(tokens, " "),
        split=[concat_tokens(ts) for ts in split(tokens)])
```

- GET
python

```
@app.route('/api/', methods=['GET'])
def api():
    text = request.args["q"]
    ret = regroup_split.process_single_line(text)
    return ret
```

    - /api/?q=...でGETに渡して動作確認
    - 自動でJSONでシリアライズされる
- POST
python

```
@app.route('/api/', methods=['GET', 'POST'])
def api():
    if request.method == "GET":
        text = request.args["q"]
    else:
        text = request.json["q"]
    ret = regroup_split.process_single_line(text)
    return ret
```

    - `$ curl -X POST -H "Content-Type: application/json" -d '{"q":"test"}' localhost:5000/api/`
    - 動作確認
    - git pushしてheroku上でも動くことを確認する

- このAPIを呼び出すクライアントサイドを作る
python

```
import requests
import json

API_URL = "https://regroup-split-server.herokuapp.com/api/"
sample_text = "あー、そうか、付箋をたくさん作ってKJ法をするプロセスに慣れてない人は、そもそもの付箋を作るところでどの程度の情報の粒度にしたらいいかがピンとこないのか。そこのところをソフトウェアが支援することが必要だな"
payload = {"q": sample_text}
r = requests.post(API_URL, json=payload)
assert r.ok
for s in r.json()["split"]:
    print(s)

"""
Expected output:
付箋をたくさん作る
KJ法をするプロセスに慣れてない人
付箋を作るところでどの程度の情報の粒度
いいかがピンとこない
ソフトウェアが支援することが必要
"""
```


- JSから呼ぶ
    - [[Flask-CORS]]
    - できた [[✅最長行をワンクリックで刻む]]

---
[[FlaskをHTTPSにする]]
