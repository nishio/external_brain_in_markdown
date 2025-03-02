---
title: "FastAPIで雑にJSONを受け取る"
---

[[FastAPI]]はハンドラの引数にパスからの情報`"/items/{item_id}"`も、クエリパラメータからの情報`?q=foobar`も、リクエストボディに積まれたJSONなどからの情報も入る。
これは型ヒントの情報を元にして振り分けられ、APIのドキュメントの自動生成などにも使われる。
これにはもちろんメリットもあるのだろうが、今回僕は他のサービスからWebhookを受け取る口を作ろうとしてたので「リクエストボディで送られてくるJSONの正確な型なんか知らんし、調べて正確に記述するのもめんどい、雑に受け取ってどんな値が来てるのか観察したい」と思った

結論
python

```
from fastapi import Body
(…snip…)
@app.post("/")
async def root(body=Body(...)):
	print(body)
```


解説

[doc](https://fastapi.tiangolo.com/tutorial/body/#request-body-path-query-parametershttps://fastapi.tiangolo.com/tutorial/body/#request-body-path-query-parameters)
> The function parameters will be recognized as follows:
>  If the parameter is also declared in the path, it will be used as a path parameter.
>  If the parameter is of a singular type (like int, float, str, bool, etc) it will be interpreted as a query parameter.
>  If the parameter is declared to be of the type of a Pydantic model, it will be interpreted as a request body.

というわけでリクエストボディから値を受け取りたければそれはPydanticである必要がある
それは困るなーという時もあり、例えば整数値が来る場合を例にしてドキュメントでも解説されている
> Without Pydantic
>  If you don't want to use Pydantic models, you can also use Body parameters. See the docs for [Body - Multiple Parameters: Singular values in body](https://fastapi.tiangolo.com/tutorial/body-multiple-params/#singular-values-in-body).

ドキュメントのサンプルは引数にPydanticが複数あるケースで説明されているので今回の目的には直接的にはマッチしない
重要な仕様:
- 引数にPydanticが一つの場合リクエストボディ全体がその引数に入る
- 引数にPydanticが複数の場合、リクエストボディから変数名のキーで得られるバリューがそれぞれの引数に入る
今回のケースはPydanticが一つなので全体が引数bodyに入る
