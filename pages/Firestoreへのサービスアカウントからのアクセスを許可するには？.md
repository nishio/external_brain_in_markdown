---
title: "Firestoreへのサービスアカウントからのアクセスを許可するには？"
---

2023-07-09
from [[Firestoreのデータを集計したい]]

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[Firestore]]へのスクリプトからのアクセスを許可するために、以下のルールを更新したいのですが。どうすればよいですか? ...
<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 現在のFirestoreルール`allow read, write: if request.auth != null && request.auth.uid == userId;`では、認証されたユーザーにアクセスを制限し、認証されたユーザーのID（request.auth.uid）がドキュメントパスのユーザーID（userId）と一致するかどうかをチェックします。
    - これにより、ユーザは自分のデータのみにアクセスできるようになります。
- しかし、Firebase Admin SDKを使用している場合、request.authオブジェクトはnullになります。
    - Admin SDK は認証にユーザーアカウントではなく、[[サービスアカウント]]を使用します。
    - このため、サーバー側のスクリプトは現在のルールではデータにアクセスできません。
- サービスアカウントからのリクエストかどうかを調べるには、 request.auth.token.firebase.sign_in_provider をチェックします。このフィールドが "null" なら、リクエストがサービスアカウントで認証されたことを意味します：
    - `|| request.auth.token.firebase.sign_in_provider == "null"`

[[Firestoreのデータを集計したい]]