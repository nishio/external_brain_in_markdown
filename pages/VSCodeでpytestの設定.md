---
title: "VSCodeでpytestの設定"
---

全然わからない
pytestをコマンドとしてではなくモジュールとして呼んで使ってたので同じことを指定してみたが詳細不明なエラーになる
.vscode/settings.json

```json
{
  "python.pythonPath": "venv/bin/python",
  "python.testing.pytestPath": "venv/bin/python -m pytest",  // here
  "python.testing.pytestArgs": [
    "tests", "--cov=server", "--cov-report=xml"
  ],
  "python.testing.unittestEnabled": false,
  "python.testing.nosetestsEnabled": false,
  "python.testing.pytestEnabled": true
}
```


では、ということでこんなシェルスクリプトを挟んでみたがこれもよくわからない結果
bash

```
#!/bin/bash
python -m pytest $* --cov=server --cov-report=xml
```


[python - Imports break VSCode testing with pytest - Stack Overflow](https://stackoverflow.com/questions/57273945/imports-break-vscode-testing-with-pytest)
ここにワークアラウンドがある
tests/__ini__.py

```
import sys
sys.path.insert(0, ".")
```


というわけでGUIでテストできるようになった。

これ、便利なのかなぁ？？
一部のテストだけ実行すると、当然それでカバーされてないところはカバレッジ的には「テストで通らない」ということになってしまう。
カバレッジを出力するためのテストをシェルスクリプトに括り出して、VSCodeからテストを走らせるときにはカバレッジ出力をしない方が良いかも。

[Testing Python in Visual Studio Code](https://code.visualstudio.com/docs/python/testing)
