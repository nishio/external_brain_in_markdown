
printでデバッグ出力して、目的のものを表示するのに手間だったから消すのを惜しく感じてコメントアウトで残し、また必要になった
- そういうのはprintではなくloggingを使うと良い
    - before
action.py

```
score = score_for_single_arg_question(env, qid, k, maxScore)
# print(repr(questions[qid](env, (k,))), k, score)
```

    - after
action.py

```
import logging
logger = logging.getLogger(__name__)
...
logger.debug((res, k, score))
```

        - ここでの本題と違うが[[✅質問候補のデバッグ表示を見やすくする]]ために関数にくくりだした

そのモジュールを呼び出す側のコードで、特定の条件が満たされた時だけログレベルをDEBUGにすると、その時だけデバッグ出力される
- action.pyの`__name__`がパッケージ階層を表現した`"server.keicho.action"`になってるので、それを使ってソースコード全体の中から一部を選んでデバッグ表示のON/OFFをできる
python

```
import logging
logging.basicConfig()
...
if some_condition:
    logging.getLogger("server.keicho.action").setLevel(logging.DEBUG)
else:
    logging.getLogger("server.keicho.action").setLevel(logging.INFO)
```

