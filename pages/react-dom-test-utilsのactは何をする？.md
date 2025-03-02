
簡潔に言えば「コールバックを呼んだ後で更新キューが空になるまでflushする」

コールバックがsyncの場合はwhile文で空になるまでflushPassiveEffectsを繰り返す。
ts

```typescript
const flushWork =
  Scheduler.unstable_flushAllWithoutAsserting ||
  function() {
    let didFlushWork = false;
    while (flushPassiveEffects()) {
      didFlushWork = true;
    }

    return didFlushWork;
  };
```


asyncの場合はflushして、キューが空になるまで自分自身をキューに積み直す。
ts

```typescript
function flushWorkAndMicroTasks(onDone: (err: ?Error) => void) {
  try {
    flushWork();
    enqueueTask(() => {
      if (flushWork()) {
        flushWorkAndMicroTasks(onDone);
      } else {
        onDone();
      }
    });
  } catch (err) {
    onDone(err);
  }
}
```


この他にも「actが二重になってないか」「asyncでないものをawaitしてないか」「asyncなのにawaitし忘れてないか」などのチェックのためのコードがある。