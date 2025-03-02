
[[Promise]]の[[await]]と[[call/cc]]はよく似ているが、call/ccは処理を止めず、Promiseは再実行できない
awaitは現在の継続を与えられたPromiseの後に接続するだけであって、継続をユーザに露出するわけではない
awaitの挙動をcall/ccで真似ることはできそうだが逆は無理そう
[[JavaScript]] [[Scheme]]
こんな記事があった
- [JavaScript + generator で Maybe、 Either、 Promise、 継続モナドと do 構文を実装し async-await と比べてみる - Qiita](https://qiita.com/legokichi/items/0582e71f4e6984548933)
- [ES2017におけるasyncとgenerator、Promise、CPS、モナドの関係 - Qiita](https://qiita.com/legokichi/items/77a36b7d2b75d8278f9d)

ts

```typescript
let p = new Promise((resolve) => {
  console.log("promise called", resolve);
  // @ts-ignore
  window.resolve = resolve;
});

(async () => {
  console.log("before await")
  console.log(await p);
  console.log("after await")
})()
// before await を表示して処理を中断

window.resolve(42)
// 42
// after await // 中断されていた処理が再開される
// undefined
window.resolve(53)
// undefined // 2回目以降は何も起こらない
```



scheme

```
(define resolve #f)
(define (p c)
	(print "promise called")
	(print c)
	(set! resolve c))

gosh> (begin
    (print "before call/cc")
    (print (call/cc p))
    (print "after call/cc"))
;before call/cc
;promise called
;#<subr "continuation">
;#<subr "continuation">
;after call/cc
;#<undef>
;処理は最後まで実行される

gosh> resolve
#<subr "continuation">

gosh> (resolve 42)
42
after call/cc
#<undef>
;再度実行される

gosh> (resolve 53)
53
after call/cc
#<undef>
;何度でも実行される 

```

