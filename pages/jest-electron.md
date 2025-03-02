---
title: "jest-electron"
---

[[jest]]のテストを[[electron]]で走らせる

- jestはブラウザではなくJSDOMを使う
- その結果canvasとかstorageを扱えない
    - `Canvas [object HTMLCanvasElement] is unable to provide a 2D context.`
- そこでelectronを使う
    - [hustcc/jest-electron: ❯ ⚛️The easiest way to run and debug test cases in electron with jest.](https://github.com/hustcc/jest-electron)
- [[create-react-app]]で作ったアプリは設定の前にejectが必要
- package.json
diff

```
+ "runner": "jest-electron/runner",
+ "testEnvironment": "jest-electron/environment",
- "testEnvironment": "jest-environment-jsdom-fourteen"
```

- これでcanvasの絡んだテストを走らせることができるようになった
- `$ DEBUG_MODE=1 npm test`
    - で、ブラウザを表示してテストを走らせることができる
    - っていうとアプリの画面が出ることを期待すると思うんだがそうではない…
    - テストが失敗した時にその画面を見るのはどうするのかな…
    - `$ npm test`
        - をした時に色々オプションをつけてもconsole.logの出力が見れなかったのだが、electron上で見ることが想定されているのかも

---

`$ npm install --save jest-electron`

need eject before config
> Out of the box, Create React App only supports overriding these Jest options:
> These options in your package.json Jest configuration are not currently supported by Create React App:
    - • verbose
    - • runner
    - • testEnvironment
> If you wish to override other Jest options, you need to eject from the default setup. You can do so by running npm run eject but remember that this is a one-way operation. You may also file an issue with Create React App to discuss supporting more options out of the box.

- `$ npx create-react-app --typescript test-jest-electron`
- `$ cd test-jest-electron/`
- `$ npm run eject`

config
- package.json
- [Configuring Jest · Jest](https://jestjs.io/docs/ja/22.x/configuration)
diff

```
+ "runner": "jest-electron/runner",
+ "testEnvironment": "jest-electron/environment",
- "testEnvironment": "jest-environment-jsdom-fourteen"
```



:

```
console.error node_modules/jest-environment-jsdom-fourteen/node_modules/jsdom/lib/jsdom/virtual-console.js:29
    Error: Not implemented: HTMLCanvasElement.prototype.getContext (without installing the canvas npm package)
```


Keep the electron browser window for debugging, set process env DEBUG_MODE=1.
- DEBUG_MODE=1 jest
`$ DEBUG_MODE=1 npm test`
