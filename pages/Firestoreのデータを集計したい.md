
2023-07-09
[[中高生のためのChatGPT]]のFirestoreのデータを集計したい

[[ローカルスクリプトでFirestoreのデータを読む]]

データを読もうとしたが読めなかった
- `db.collection('users').get()`したがsnapshot.sizeはゼロ
- 原因を聞いた
    - いくつか原因が挙げられたので上からチェック
    - 「ルールがおかしいのでは？」と言われたのでルールを貼って確認してもらう
    - [[Firestoreへのサービスアカウントからのアクセスを許可するには？]]

ルールを変更しても読めなかった
- 具体的なメッセージを1件取得するコードを作ったらできた
- でも `db.collection('users').get()`したがsnapshot.sizeはゼロ

もう一度考えて「サービスアカウントに普通のユーザと同じアクセス権を付与してもユーザの一覧取得はできないじゃん」と気づいた
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>snapshot.size is zero. I just noticed that the rule deny traversal. Fix it
- <img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>`allow list: if request.auth.token.firebase.sign_in_provider == "null";`

それでもダメ、末端のオブジェクトを取得できるのに親をトラバーサルできない現象がなぜ起こるのか理由を聞いた
- <img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>No user document: When you fetch a nested sub-collection document directly (as in code A), Firestore doesn't need the parent document to exist. In other words, even if there's no document at users/{userId}, you can still fetch a document at users/{userId}/rooms/{roomId}/messages/{messageId}.
- [Firebase コンソールでの Cloud Firestore の管理](https://firebase.google.com/docs/firestore/using-console?hl=ja&authuser=0&_gl=1*1y83w4p*_ga*MTQ5MDA3NDc1MS4xNjg2MDI5OTU3*_ga_CW55HF8NVT*MTY4ODgyODA1My4xNi4xLjE2ODg4MzM2NDguMC4wLjA.#non-existent_ancestor_documents)
- > 祖先が存在しない場合であっても、ドキュメントは存在できます。
- これか...

祖先ドキュメントが存在しない時に子孫ドキュメントを列挙するには？
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> How to get all `/users/<user_id>/rooms/<room_id>` when `/users/<user_id>` is not exists.
- <img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/> There is a way to fetch all rooms from all users using a Firestore feature called Collection Group Queries.
    - `db.collectionGroup('rooms').get()`
    - できた

そのroomがどのユーザに属しているかはどうやって知る？
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Given doc, how can I see its parent <user_id>
- <img src='https://scrapbox.io/api/pages/nishio/gpt-4/icon' alt='gpt-4.icon' height="19.5"/> `doc.ref.parent.parent.id`

後は集計するだけ！めでたしめでたし！
