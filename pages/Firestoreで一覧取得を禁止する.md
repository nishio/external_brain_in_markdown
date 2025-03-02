---
title: "Firestoreで一覧取得を禁止する"
---

[[Firestore]]のセキュリティルールは最初はこうなっている
:

```
match /{document=**} {
  allow read, write;
}
```


このread権限はgetとlistに分けられる。このlist権限を制限すれば一覧の取得を禁止できる。
:

```
match /{document=**} {
  allow get;
  allow list: if false;
  allow write;
}
```


セキュリティを絞る前は下記のコードが成功していたが、絞ると期待通りエラーになる
:

```
firebase.firestore().collection("collection_foo").get().then((qs) => {
  qs.forEach((d) => console.log(d.id));
});
// Uncaught (in promise) FirebaseError: Missing or insufficient permissions.
```


doc [https://firebase.google.com/docs/firestore/security/rules-structure](https://firebase.google.com/docs/firestore/security/rules-structure)

[[Capability URL]]
