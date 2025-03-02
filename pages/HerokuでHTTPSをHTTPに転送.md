
Webhookを受け取ってちょっとした処理をやりたかった
- その処理をするサーバXでHTTPSのサーバを立ち上げるのは証明書の管理がめんどくさいからやりたくない
- Herokuで受け取ってHTTPでサーバXに転送した
- (やってから思ったけどLambdaでも良かったかも)

python

```
from flask import Flask, request
import requests
app = Flask(__name__)


def create_app():
    return app


@app.route('/', methods=['GET', 'POST'])
def root():
    if request.is_json:
        print(request.json)
        requests.post("http://...../", json=request.json)
    return "OK" 
```


関連
- [[Heroku+Flask]]
