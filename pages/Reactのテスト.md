---
title: "Reactのテスト"
---

- [テスト概要](https://ja.reactjs.org/docs/testing.html)
    - > React コンポーネントは他の JavaScript のコードと同じようにテストできます。
- [テストのレシピ集](https://ja.reactjs.org/docs/testing.html)
    - > React コンポーネントのための一般的なテストのパターン集です。
    - React製のアプリをJestでテストする方法の良い解説
    - `jest.spyOn` [doc](https://jestjs.io/docs/ja/jest-object#jestspyonobject-methodname)
        - メソッドをモックに置き換える
        - 実装が与えられなかった時、デフォルトで元の実装を使う
            - 実装の与え方 `jest.spyOn(object, methodName).mockImplementation(() => customImplementation)`
        - 元の実装を使うモックに何の意味があるか？
            - そのモックがどんな引数で呼ばれたか、どんな値を返したか、例外を投げたか、などが観察可能になる [doc](https://jestjs.io/docs/ja/mock-function-api)
        - 「メソッド」と呼ばれてるが、クラスのメソッドには限らない、モジュールのトップレベル関数を書き換えるときはモジュールに名前をつけてインポートすれば良い
            - `import * as fooModule from './foo';`
        - setter / getter もスパイできる [doc](https://jestjs.io/docs/ja/jest-object#jestspyonobject-methodname-accesstype)
    - `jest.mock`でモジュールを丸ごとモックに置き換えることもできる [doc](https://jestjs.io/docs/ja/jest-object#jestmockmodulename-factory-options)
    - イベントを投げるときはバブルが必要
    - タイマーを使う処理はタイマーをモックする
    - スナップショットテスト [doc](https://jestjs.io/docs/ja/snapshot-testing)
        - スナップショットを取ってくれて、それと相違してるかチェックしてくれる
        - 別ファイルに保存するものと、テストコード中に埋め込むものがある
        - DOMに限らない
        - 意図的な変更によってスナップショットと一致しなくなったときは`jest --updateSnapshot`
        - 例えば生成日時などのスナップショットごとに変化する値は、第一引数`propertyMatchers`でフィルタする [doc](https://jestjs.io/docs/ja/snapshot-testing#property-matchers)

- `mockFn.mockImplementationOnce` [doc](https://jestjs.io/docs/ja/mock-function-api#mockfnmockimplementationoncefn)
    - 一回だけ実装を差し替える

- [テストユーティリティ – React](https://ja.reactjs.org/docs/test-utils.html)
    - [React Testing Library | Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
        - ユーザが実際に使う状態に近いテストをする
        - →ユーザはDOMのラベルを見てボタンを押す
        - Enzymeの後継
        - [[Mock Service Worker]]


- [テスト環境](https://ja.reactjs.org/docs/testing-environments.html)
    - > このドキュメントではあなたの環境に影響する要素や、いくつかのシナリオにおける推奨事項について概説します。



[[React]]の[[テスト]]
