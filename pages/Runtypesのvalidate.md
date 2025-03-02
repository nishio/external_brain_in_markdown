---
title: "Runtypesのvalidate"
---

今までユーザがJSONファイルをインポートしようとした時に、インポートされるアイテムごとに「isTItemがfalseだったらinvalid itemと表示する」ぐらいのことしかできてなかった
- [[Runtypes]]に移行したら「何がミスマッチなせいでfalseなのか」がdetailsの中に入ってた
- これをユーザに見せればそのJSONの何が悪いのかわかりやすくて良いな

ts

```typescript
  const result = RTItem.validate({
    type: "kozane",
    position: [],
    id: "A",
    text: "A",
  });
  if (!result.success) {
    console.log(result.details);
  }
```

:

```
 console.log
   {
     position: 'Failed constraint check for [number, number]: Expected length 2, but was 0',
     scale: 'Expected number, but was missing'
   }
```

