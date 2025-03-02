
[[Firebase]]で[[レンジクエリ]]
- 過去24時間の投稿
- 特定の日の投稿
を得たい

> まず、orderByChild()、orderByKey()、orderByValue() のいずれかの並べ替え関数を使用
> 次に、これらを他の 5 つのメソッド limitToFirst()、limitToLast()、startAt()、endAt()、equalTo() と組み合わせて複雑なクエリを実行できます。
[https://firebase.google.com/docs/database/admin/retrieve-data#section-queries](https://firebase.google.com/docs/database/admin/retrieve-data#section-queries)

> 開発用にはインデックスは不要:
>  REST API を使用する場合を除いて、開発用にはインデックスは不要です。リアルタイムのクライアント ライブラリではインデックスを指定せずにアドホック クエリを実行できます。
[データのインデックス作成  |  Firebase Realtime Database](https://firebase.google.com/docs/database/security/indexing-data)

[データの取得  |  Firebase Realtime Database](https://firebase.google.com/docs/database/admin/retrieve-data#section-ordered-data)
