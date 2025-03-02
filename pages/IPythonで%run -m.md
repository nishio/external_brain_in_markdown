---
title: "IPythonで%run -m"
---

IPythonで`%run foo.py -t`してたけど`%run -m foo -t`にしていく方が、他のプロジェクトから部品として使うフェーズになってくると便利か
- 前者は相対インポートができない
    - > What you probably did is you tried to run moduleX or the like from the command line. When you did this, its name was set to __main__, which means that relative imports within it will fail, because its name does not reveal that it is in a package.
        - [python - Relative imports for the billionth time - Stack Overflow](https://stackoverflow.com/questions/14132789/relative-imports-for-the-billionth-time/14132912#14132912)
- 後者はインポートされた時と同様にモジュールとして実行される
    - つまり相対インポートできる


venvやunittestも`-m`してるし。


あー。このスタイルの場合、実行されたスクリプトのグローバルスコープがipythonの側のスコープと別になるのか
- 適当に関数を置いといて必要に応じて呼ぶことができない
- ちゃんとargsで呼び分ける？
    - そもそも内部状態を観察したいとかの時にこれではできない
- 単にコマンドのエントリポイントを変えたいだけならそもそもスクリプト自体分けたらいいのでは説

[[-m pytest]]
