---
title: "WebWorker"
---

- [[ServiceWorker]]とは違う
- 重たい処理をUIスレッドとは別のスレッドで動かすことで、処理中にUIがフリーズすることを防げる
- 情報のやり取りはメッセージパッシング

- WebWorkerを作る時に本体とは別のJSを作る必要がある
    - `var myWorker = new Worker('worker.js');`
    - [Using Web Workers - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
- だが、本体とコードを共有したい
    - TSの型定義とかDOMに触らないユーティリティ関数とか
    - なお前提として、僕はTypeScriptで実装したい
- できた
    - [https://github.com/nishio/tutorial-webworker-with-react/blob/master/README.md](https://github.com/nishio/tutorial-webworker-with-react/blob/master/README.md)



----memo
2020-03-16-2
- Cannot find module 'worker-loader!./webworker'.  TS2307
    - `import Worker from "worker-loader!./webworker";`
- [https://stackoverflow.com/questions/53818157/using-webpack-worker-loader-with-typescript-causes-cannot-find-module-error](https://stackoverflow.com/questions/53818157/using-webpack-worker-loader-with-typescript-causes-cannot-find-module-error)
    - typing/custom/index.d.ts

Uncaught TypeError: Failed to execute 'postMessage' on 'DedicatedWorkerGlobalScope': No function was found that matched the signature provided.

2020-03-16
- 2020-03-10の実験を踏まえて
    - 生のwebpackでは複数のエントリーポイントから複数のファイル出力ができた
    - create-react-appで作られたwebpack.config.jsを修正することを試みる
    - [https://github.com/nishio/learn-ww-wp-cra-t/commit/2b85f2fefb37d102989229b596622fee31632a47](https://github.com/nishio/learn-ww-wp-cra-t/commit/2b85f2fefb37d102989229b596622fee31632a47)
    - 複数ファイルを出すことはできた
- 問題点
    - 指定した出力ファイル名がそのまま使われない
        - chunkに分けたり、ハッシュ値を付与したりする
        - これは最悪disableする手がある
    - 出力ファイルがそのまでは使えない
        - webworker APIはスクリプトのトップレベルにon messageがあることを期待してるが、実際に出力されるのは下記
        - これはes2015のmodule構文がbabelとwebpackを介してブラウザでも実行できる形に変換されたもの
        - 今必要なのは「この仕組みでインポートできる」「onmessageはこの仕組みで包まずにグローバル空間に露出させる」の組み合わせ
            - どうやるのか？？
            - [Shimming | webpack](https://webpack.js.org/guides/shimming/)?
            - ここでworker-loaderでは
            - ここまでの積み重ねでworker-loaderが理解できるようになった！
ts

```typescript
(this["webpackJsonplaern-ww-wp-cra-t"] = this["webpackJsonplaern-ww-wp-cra-t"] || []).push([["webworker"],{

/***/ "./src/webworker.ts":
/*!**************************!*\
  !*** ./src/webworker.ts ***!
  \**************************/
/*! exports provided: onmessage */
/***/ (function(module, __webpack_exports__, __webpack_require__) {

"use strict";
__webpack_require__.r(__webpack_exports__);
/* harmony export (binding) */ __webpack_require__.d(__webpack_exports__, "onmessage", function() { return onmessage; });
console.log("webworker");
const onmessage = function (e) {
  console.log("Message received from main script", e);
  console.log("Posting message back to main script");
  postMessage(e, "*");
};

/***/ }),

/***/ 2:
/*!************************************************************!*\
  !*** multi (webpack)/hot/dev-server.js ./src/webworker.ts ***!
  \************************************************************/
/*! no static exports found */
/***/ (function(module, exports, __webpack_require__) {

__webpack_require__(/*! /Users/nishio/learn-ww-wp-cra-t/node_modules/webpack/hot/dev-server.js */"./node_modules/webpack/hot/dev-server.js");
module.exports = __webpack_require__(/*! /Users/nishio/learn-ww-wp-cra-t/src/webworker.ts */"./src/webworker.ts");


/***/ })

},[[2,"runtime-webworker",2]]]);
//# sourceMappingURL=webworker.chunk.js.map
```


2020-03-10
昨日の議論を経て、webpackを掘り下げるのがよいと判断した
- まずは実験用に小さいプロジェクトを作る
- 参考: [Getting Started | webpack](https://webpack.js.org/guides/getting-started/)
- コマンドラインで直接webpackを叩いて、bundle.jsができるのを確認

webpackの設定でエントリーポイントを指定することができる(たとえばindex.ts)
- メインのスクリプト用のエントリポイントとワーカー用のエントリーポイントを2つ用意したらよいのではないか
- [Multi Page Application](https://webpack.js.org/concepts/entry-points/#multi-page-application)
webpack.config.js

```javascript
module.exports = {
  entry: {
    index: "./src/index.ts",
    webworker: "./src/webworker.ts"
  },
  ...
    output: {
      filename: "[name].js",
      path: path.resolve(__dirname, "dist")
    },
```


:

```
$ ~/node_modules/webpack-cli/bin/cli.js 
Hash: def769ed43f728038706
Version: webpack 4.42.0
Time: 808ms
Built at: 2020/03/16 18:02:28
       Asset     Size  Chunks             Chunk Names
    index.js  4.1 KiB       0  [emitted]  index
webworker.js  4.4 KiB       1  [emitted]  webworker
Entrypoint index = index.js
Entrypoint webworker = webworker.js
[0] ./src/common.ts 53 bytes {0} {1} [built]
[1] ./src/index.ts 82 bytes {0} [built]
[2] ./src/webworker.ts 265 bytes {1} [built]
```


3つのTSから2つのJSが出力されて、それぞれにcommon.tsで定義したものが含まれてる
ゼロから作るプロジェクトならこれで良さそう
create-react-appで作ったプロジェクトではentryがarrayなので、そこをどうにかする必要がある
- > What happens when you pass an array to entry? Passing an array of file paths to the entry property creates what is known as a "multi-main entry". This is useful when you would like to inject multiple dependent files together and graph their dependencies into one "chunk".
    - [Entry Points | webpack](https://webpack.js.org/concepts/entry-points/)

webpack.config.js

```javascript
    entry: [
      isEnvDevelopment &&
        require.resolve("react-dev-utils/webpackHotDevClient"),
      // Finally, this is your app's code:
      paths.appIndexJs
    ].filter(Boolean),
    output: {
      ...
      filename: isEnvProduction
        ? "static/js/[name].[contenthash:8].js"
        : isEnvDevelopment && "static/js/bundle.js", 
```


条件分岐を設定ファイルに詰め込んでてゴチャゴチャしてるが、プロダクション環境だとファイル名にハッシュをつけてキャッシュされないようにしている
このファイル名を取得する方法が必要だ

---2020-03-09
create-react-appでテンプレ作ってるのでwebpackはブラックボックスになっちゃってる
まずejectして、設定を書き換えられるようにする
新しいプロジェクトで試そう
`$ npx create-react-app --typescript learn-webworker`
`$ cd learn-webworker/`
`$ npm run eject`
:

```
> learn-webworker@0.1.0 eject /Users/nishio/learn-webworker
> react-scripts eject

NOTE: Create React App 2+ supports TypeScript, Sass, CSS Modules and more without ejecting: https://reactjs.org/blog/2018/10/01/create-react-app-v2.html

? Are you sure you want to eject? This action is permanent. Yes

Ejecting...

Copying files into /Users/nishio/learn-webworker
  Adding /config/env.js to the project
  ...
  Adding /config/webpack.config.js to the project
  ...

Updating the dependencies
  Removing react-scripts from dependencies
  ...
  Adding webpack to dependencies
  ...

Updating the scripts
  Replacing "react-scripts start" with "node scripts/start.js"
  Replacing "react-scripts build" with "node scripts/build.js"
  Replacing "react-scripts test" with "node scripts/test.js"

Configuring package.json
  Adding Jest configuration
  Adding Babel preset

...
Ejected successfully!

Staged ejected files for commit.

Please consider sharing why you ejected in this survey:
  http://goo.gl/forms/Bi6CZjk1EqsdelXk1
```


`$ git status`
:

```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   config/env.js
        ...
        new file:   config/webpack.config.js
        ...

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   package-lock.json
        modified:   package.json
        modified:   src/react-app-env.d.ts
```


`$ git add -u`
`$ git commit -m "eject"`
`$ npm install worker-loader --save-dev`

[https://github.com/nishio/learn-webworker/blob/04fe485/config/webpack.config.js#L362-L392](https://github.com/nishio/learn-webworker/blob/04fe485/config/webpack.config.js#L362-L392)
- これを書き換える必要がありそうだ
- [ecmascript 6 - How to use webpack babel-loader and es6 with worker-loader? - Stack Overflow](https://stackoverflow.com/questions/40323032/how-to-use-webpack-babel-loader-and-es6-with-worker-loader?fbclid=IwAR2tzXNRmbKmUYVkhGbMW0BqTtVi1IJQOoUxDRyCUez9fdsL6QNPq3Kkb5c)
:

```
{
    test: /\.worker\.js$/,
    loader: "worker!babel?presets[]=es2015"
}
```

- → Cannot find module: 'worker!babel?presets[]=es2015'. Make sure this package is installed.

[https://github.com/nishio/learn-webworker/blob/4d426fe/config/webpack.config.js#L363](https://github.com/nishio/learn-webworker/blob/4d426fe/config/webpack.config.js#L363)
→ Cannot find module: 'worker-loader!babel-loader'. Make sure this package is installed.

うーむ、webpackのルールの書き方の問題かな
参考にした情報が古くて今のwebpackでは別の書き方が必要とかありそう

[babel/babel-loader: 📦 Babel loader for webpack](https://github.com/babel/babel-loader)
[webpack-contrib/worker-loader: A webpack loader that registers a script as a Web Worker](https://github.com/webpack-contrib/worker-loader)
- [How to use with babel-loader ? · Issue #35 · webpack-contrib/worker-loader](https://github.com/webpack-contrib/worker-loader/issues/35)

-----過去のメモ
- [zlepper/typescript-webworker: An example repository for using typescript and webworkers with webpack](https://github.com/zlepper/typescript-webworker)
- `const worker = new Worker(workerPath);`
    - という形で個別ファイルの読み込みが必要
    - デフォルトの設定だと一つのファイルにまとめられてしまう
- `import * as workerPath from "file-loader?name=[name].js!./test.worker";`
    - こうやってWebpackに、個別のファイルにするよう指示する
- しかしこのやり方は[[ESLint]]に怒られる
    - `import/no-webpack-loader-syntax`
- `// eslint-disable-next-line import/no-webpack-loader-syntax`
    - 無視してみた
- exportあり
    - `Uncaught SyntaxError: Unexpected token 'export'`
- exportなし
    - `All files must be modules when the '--isolatedModules' flag is provided.  TS1208`
- TSなのがいけないのか？JSにしてみる
js

```javascript
// eslint-disable-next-line no-restricted-globals
addEventListener("message", message => {
  console.log("Message received from main script");
  console.log("in webworker", message.data);
  postMessage("this is the response " + message.data * 2);
});
```

OK、動いた

しかし他のファイルをインポートしようとするとエラー
- `Uncaught SyntaxError: Cannot use import statement outside a module`


...

- [ES-Lint Rule "import/no-webpack-loader-syntax" please deactivate · Issue #1015 · facebook/create-react-app](https://github.com/facebook/create-react-app/issues/1015)
- [Customize webpack configuration of React App created with Create-react-app](https://medium.com/@ryoldash/customize-webpack-config-of-react-app-created-with-create-react-app-7a78c7849edc)
- [javascript - where is create-react-app webpack config and files? - Stack Overflow](https://stackoverflow.com/questions/48395804/where-is-create-react-app-webpack-config-and-files)
