---
title: "storeのsubscribeとuseEffect"
---

from [[pRegroup-done-2019]]
storeのsubscribeとuseEffect
storeのsubscribeとuseEffectが意味合い的に重複しているけどどっちをどう使うのが良いのか
こんな感じで良いのかlistenerにした方がいいのか
ts

```typescript
 useEffect(() => {
   ...
 }, [store.getState().items]);
```


subscribeの説明を読む
[https://redux-docs.netlify.com/api/store#a-id-subscribe-class-anchor-a-subscribelistener-subscribe](https://redux-docs.netlify.com/api/store#a-id-subscribe-class-anchor-a-subscribelistener-subscribe)
> It is a low-level API. Most likely, instead of using it directly, you'll use React (or other) bindings. If you commonly use the callback as a hook to react to state changes, you might want to write a custom observeStore utility. The Store is also an Observable, so you can subscribe to changes with libraries like RxJS.
