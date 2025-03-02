---
title: "Promise"
---

[Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[How do Promises Work? - Quil's Fluffy World](https://robotlolita.me/articles/2015/how-do-promises-work/)
- 日本語訳: [Promiseはどう動作するのか – Promiseを実装してみる | POSTD](https://postd.cc/how-do-promises-work/)
良い解説だが日本語訳はあまり良くない



2019/6に[Promise - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)に対して
- > 「resolveが非同期的に呼ばれる」という言葉は曖昧だ
と書いたが、今見たらその表現が見つけられなかった。
2021/2現在、もっと明確に書かれている。
- > プロミスは非同期であることが保証されていることに注意してください。したがって、既に「解決済み」のプロミスに対するアクションは、スタックがクリアされ、クロックティックが経過した後にのみ実行されます。この効果は setTimeout(action,10) とよく似ています
---old
「resolveが非同期的に呼ばれる」という言葉は曖昧だ
- Promiseの第一引数である(resolve, reject) => {...}の中でresolveを同期的に呼ぼうが非同期的に呼ぼうが、thenの第一引数に渡された関数は非同期的に呼ばれる

:

```
create promise start
promise body start
sync body start
sync body end
promise body end
create promise end
specify promise.then start
specify promise.then end
resolved ok
```


ts

```typescript
  const syncBody = (resolve: any, reject: any) => {
    console.log("sync body start")
    resolve("ok")
    console.log("sync body end")
  }
  const asyncBody = (resolve: any, reject: any) => {
    console.log("async body start")
    setTimeout(() => {
      console.log("timeout start")
      resolve("ok")
      console.log("timeout end")
    }, 1000)
    console.log("async body end")
  }

  console.log("create promise start")
  let p = new Promise((resolve, reject) => {
    console.log("promise body start")
    syncBody(resolve, reject)
    console.log("promise body end")
  })
  console.log("create promise end")

  console.log("specify promise.then start")
  p.then((x) => {
    console.log("resolved", x)
  })
  console.log("specify promise.then end")
```



