---
title: "Firestoreでオフライン判定"
---

単体ではできない。
→別アイデア:トランザクションはオフラインの時に必ず失敗するのでそれを使う手があるかも

see: [Cloud Firestore でプレゼンスを構築する  |  Firebase](https://firebase.google.com/docs/firestore/solutions/presence)

[[Realtime Database]]なら'.info/connected'っていう特殊パスがある
js

```javascript
firebase.database().ref('.info/connected').on('value', function(snapshot) {
   // If we're not currently connected, don't do anything.
   if (snapshot.val() == false) {
       return;
   };
   ...
```


[[Cloud Firestore]]では？
> 接続性 - この実装は Cloud Firestore ではなく Realtime Database との接続性を測定します。
公式ドキュメントですらCloud Firestoreで解決せず、Realtime Database との接続性チェックで代用してる
