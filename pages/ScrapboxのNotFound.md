
プロジェクトがない時
- `{"name":"NotFoundError","message":"Project is not found"}`
- 404

ページがない時
- `{"name":"NotFoundError","message":"Page not found","details":{"linkTo":"https://scrapbox.io/nishio/"}}`
- 404

- 赤リンクの時
- 普通にレスポンスが帰ってくる
    - 200
- 見分けるポイントはこれかな？
    - `"persistent": false`

