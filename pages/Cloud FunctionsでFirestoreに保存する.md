
公式のサンプルがあるのでそれを見ると良い
[functions-samples/quickstarts/uppercase-firestore at main · firebase/functions-samples · GitHub](https://github.com/firebase/functions-samples/tree/main/quickstarts/uppercase-firestore)

[コード](https://github.com/firebase/functions-samples/blob/main/quickstarts/uppercase-firestore/functions/index.js)を見て思ったこと
- exportsの外で`admin.initializeApp();`するのか、なるほど
- `functions.https.onRequest(async (req, res) => { ... })`とasync関数にすることで`const writeResult = await ...`と結果をawaitできるわけか、なるほど

[[Cloud Functions]]で[[Firestore]]に保存する