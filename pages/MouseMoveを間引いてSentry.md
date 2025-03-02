---
title: "MouseMoveを間引いてSentry"
---

Regroupのテスト自動化をする上で「ドラッグして囲う」というユーザの操作を記録し再現したい。しかしMouseMove系のイベントは大量に出るのですべて記録したくはない。
![image](https://gyazo.com/e228c23fff2d61bc95430876234ac701/thumb/1000)
そこで「直前がMouseMove系のイベントであり、かつ500ms以内なら記録しない」とやることにした。記録先はリングバッファになっていて直近の100件だけが保持される。
ts

```typescript
export const push = (data: IHasType) => {
  if (data.type === "Drag") {
    if (prevEvent?.type === "Drag") {
      if (Date.now() - prevEventTime < 500) {
        prevEventTime = Date.now();
        prevEvent = data;
        return;
      }
    }
  }
  prevEventTime = Date.now();
  prevEvent = data;
  
  const json = JSON.stringify(data);
  if (ringBuffer.length < MAX_RECORD_NUM) {
    ringBuffer.push(json);
  } else {
    ringBuffer[index] = json;
    index = (index + 1) % MAX_RECORD_NUM;
  }
};

export const get = () => {
  return ringBuffer.slice(index).concat(ringBuffer.slice(0, index));
};
```


メニューに「Sentryに送る」を付けた。Sentry上で下記のように取得できる。
![image](https://gyazo.com/6f055b05a6732fabdb59455fcb1476d2/thumb/1000)


追記
- せっかく作ったのだけど、テストする時のデフォルトのキャンバスサイズが小さかったので手で数値をいじってて「あれ？これだったら最初から手打ちで良かったのでは？」となった
- まあ、これをやることでどんなイベントがどんな順で起きてるのか理解したからやりやすくなったのだとも言える
- Sentryに送ることは開発環境以外の場所で起こった問題を記録できるメリットがあるが、開発環境ではconsole.logで直接観察するのの方が操作してすぐに観察できていい
- イベントハンドラでconsole.logするとmove系イベントが大量になるから、その意味では今回の時間で間引く方法は良い
