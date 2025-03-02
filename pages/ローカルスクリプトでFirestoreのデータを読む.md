---
title: "ローカルスクリプトでFirestoreのデータを読む"
---

2023-07-09
1:
- `$ npm init -y`
2:
- `$ npm install firebase-admin --save`
3:
js

```javascript
const admin = require('firebase-admin');
let serviceAccount = require('path/to/serviceAccountKey.json');

admin.initializeApp({
  credential: admin.credential.cert(serviceAccount)
});

let db = admin.firestore();
```

4:
- `$ node yourScript.js`

1をスルーしたせいでプロジェクトのnode_modulesに追加しようとして依存関係のエラーが起きた
- 別にプロジェクトの他のソースを動かすわけではないのでサブフォルダで1をすればよい

`let serviceAccount = require('path/to/serviceAccountKey.json');`
- これのpathは`'./foobar-fffff-firebase-adminsdk-xxxxx-xxxxxxxx.json'`みたいなのになる
    - `./`をつけてなくてerror

