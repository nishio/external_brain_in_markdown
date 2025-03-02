---
title: "Firestoreからまとめて削除"
---

Chrome devtoolでやった
js

```javascript
let querySnapshot;
db.collection("kakidashi").get().then((qs) => { querySnapshot = qs})
querySnapshot.docs[0].data().items
querySnapshot.forEach((x) => {
	if(x.data().items.length == 0){
	  x.ref.delete()
	}
})
```


[[Firestore]]

