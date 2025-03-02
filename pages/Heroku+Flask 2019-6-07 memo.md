
from [[Heroku+Flask]]
Heroku+Flask 2019-6-07 memo
`$ heroku buildpacks:set heroku/python`
必要なファイルを追加してgit push heroku master
- new file:   Procfile
- new file:   requirements.txt
- new file:   runtime.txt
してるのに"App not compatible with buildpack"になるなぁ
- と思ってたが、git add しただけでcommitしてなかったw


- Procfileに`web:FLASK_APP=server.py flask run --port 8000`とか書いたが、flaskが起動したものすぐ殺されてしまう
log

```
019-06-06T16:06:39.226032+00:00 heroku[web.1]: Starting process with command `FLASK_APP=server.py flask run --port 3000`
2019-06-06T16:06:41.580063+00:00 app[web.1]:  * Serving Flask app "server.py"
2019-06-06T16:06:41.580088+00:00 app[web.1]:  * Environment: production
2019-06-06T16:06:41.580091+00:00 app[web.1]:    WARNING: This is a development server. Do not use it in a production deployment.
2019-06-06T16:06:41.580137+00:00 app[web.1]:    Use a production WSGI server instead.
2019-06-06T16:06:41.580145+00:00 app[web.1]:  * Debug mode: off
2019-06-06T16:06:43.000795+00:00 app[web.1]:  * Running on http://127.0.0.1:3000/ (Press CTRL+C to quit)
2019-06-06T16:07:17.795885+00:00 heroku[router]: at=error code=H20 desc="App boot timeout" method=POST path="/" host=yagokoro.herokuapp.com request_id=3c62ce00-bbe8-4ac9-8ad7-b608b884c188 fwd="163.43.120.164" dyno= connect= service= status=503 bytes= protocol=https
2019-06-06T16:07:39.290453+00:00 heroku[web.1]: Error R10 (Boot timeout) -> Web process failed to bind to $PORT within 60 seconds of launch
2019-06-06T16:07:39.290453+00:00 heroku[web.1]: Stopping process with SIGKILL
2019-06-06T16:07:39.394293+00:00 heroku[web.1]: State changed from starting to crashed
2019-06-06T16:07:39.376614+00:00 heroku[web.1]: Process exited with status 137
```


他の記事を参考にgunicornを挟んでみることにした
- なぜこれが必要なのかはよくわからない
- 参考: [Re:ゼロからFlaskで始めるHeroku生活 〜環境構築とこんにちは世界〜 - Qiita](https://qiita.com/ymgn_ll/items/96cac1dcf388bc7a8e4e)

ログに下のように出るから5119番にOutgoing Webhookすべきなのかと思ったが、80番でよかった
- > Listening at: [http://0.0.0.0:5119](http://0.0.0.0:5119)

とりあえずこれで固定のURLで僕のマシンの状態に関わらず繋がるようになった

