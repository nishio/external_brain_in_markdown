---
title: "Flask Blueprint"
---

python

```
from flask import Flask, Blueprint

bp = Blueprint('server', __name__)


def create_app():
    app = Flask(__name__)
    app.register_blueprint(bp)
    return app


@bp.route('/', methods=['GET'])
def root():
    return "OK"
```


app.routeでルーティングをやるのがミニマルなのだけど、ファイルを分けたくなったときにやりにくいので、blueprintを作っておいて後からappに追加する
