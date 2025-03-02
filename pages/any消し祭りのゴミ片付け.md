
2021-02-18
先日のRegroupから[[2日掛けてanyを撲滅した]]件、やはり型のテストだけでは問題を全部発見することはできておらず[[Sentry]]にエラー報告が上がってきている
![image](https://gyazo.com/f20acbd51bf9916b0546eeb288de68b4/thumb/1000)

まずは一番多い`Error neverComeHere(assertion) Unhandled InitialState * onDrag`を見ていこう
これは不整合が起きた時に早めに気づけるようにとassertしてるものなのだが、開発者が気づかなかった。
![image](https://gyazo.com/3515a0bbce298490cd68d418928f1a50/thumb/1000)
うーむ、何が原因か、とブレッドクラムを遡ってみたらlassoに切り替えてるのがわかった
![image](https://gyazo.com/f9ea011adeb463470ed9190eb24b6ff9/thumb/1000)
lassoに切り替えて試したら手元でも問題が再現した。メッセージは違って
`ReferenceError: paper is not defined`
とのこと。これは
`const paper = require("paper");`
を忘れてることによる。(え？これ型チェックで発見されないの？)

メモ
- なぜ型チェックで発見されないのか？
- lassoに切り替えて動作確認すべき(自動テストで)

そこを直すと別のエラー
`TypeError: Cannot read property 'children' of undefined`
これも似た問題(追記: 誤認です)
Regroupを書き始めた時、どこからでもpaperにアクセスする方法がわからなくてwindowにぶら下げてた。
`const items = window.app.paper.projects[0].layers[0].children;`

`const paper = require("paper");`

Typescipt doc: [export = and import = require()](https://www.typescriptlang.org/docs/handbook/modules.html#export--and-import--require)をみて
`import paper = require("paper");`にしたらエラー
error

```
SyntaxError: /Users/nishio/regroup/src/onOverlayCanvas.ts: `import =` is not supported by @babel/plugin-transform-typescript
Please consider using `import <moduleName> from '<moduleName>';` alongside Typescript's --allowSyntheticDefaultImports option.
> 2 | import paper = require("paper");
```


素直な`import paper from "paper";`でちゃんと動いた。なんだこれでよかったのか。

JavaScriptにモジュールの仕組みが発達する前の知識で、JavaScriptのサードパーティライブラリをJavaScript向けの解説を読みながらTypeScriptの中で使ったことで不必要にレガシーな書き方をしてしまっていた。
検索したら`var paper = require("paper");`なんてのまであった。varを使うなんて！

`window.app.paper`を`import paper from "paper";`に変えていく。
おや、新しい型エラーだ
ts

```typescript
Argument of type 'HTMLElement | null' is not assignable to parameter of type 'string | HTMLCanvasElement'.
  Type 'null' is not assignable to type 'string | HTMLCanvasElement'.  TS2345

    50 |     // Get a reference to the canvas object
    51 |     const canvas = document.getElementById("myCanvas");
  > 52 |     paper.setup(canvas);
```


なるほど、requireしたものはanyだったのか！
![image](https://gyazo.com/43abf964f3c73d9c357cf5623b045d3e/thumb/1000)

片付け終わったけど問題は解決してない
えーと、じっくり見てみると、これはまだ何も描画してない状態ではレイヤーが存在しないってことだから、無ければ空リストにすれば良いか
`const items = paper.projects[0].layers[0]?.children ?? [];`


`Property 'onDeactivate' does not exist on type 'Tool'.`
`Property 'getBounds' does not exist on type 'PointText'.`
`Property 'getBounds' does not exist on type 'Layer'.`

