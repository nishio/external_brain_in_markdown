---
title: "Sentryでパフォーマンス計測"
---

from [[Sentry Memo]]
Sentryでパフォーマンス計測
- [Included Instrumentation for React | Sentry Documentation](https://docs.sentry.io/platforms/javascript/guides/react/performance/included-instrumentation/)
    - パフォーマンス計測ができるようになった
ts

```typescript
export const getNewTalkID = () => {
  const transaction = Sentry.startTransaction({ name: "getNewTalkID" });
  const span = transaction.startChild({ op: "getNewTalkID" });

  fetch(...)...
    .then((text) => {
    	  ...
          span.finish();
          transaction.finish();
        });
    })
    .catch(() => {
      Sentry.captureMessage("ERROR_ON_SERVER: getNewTalkID");
      ...
    });
};
```


![image](https://gyazo.com/9a4ebf11d8c86978e0194989da897c9c/thumb/1000)

フィルタをp100にすると外れ値も含めて遅い順にでる
この例だと16秒掛かってる外れ値が1件ある
実はこれが知りたかった(サーバがスリープしていてリクエストを受けてから起こす時にかかる時間)
![image](https://gyazo.com/a3fbe8c76d001c7c4e489a9503dd75e3/thumb/1000)
