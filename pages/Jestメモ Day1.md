---
title: "Jestメモ Day1"
---

from [[Jestメモ]]
Jestメモ Day1
2021-02-15
- [[vscode-jest]]を入れる
    - 自動でwatchし始める
- いきなり[[create-react-app]]のデフォルトのテストがこける
    - 「undefinedはmapを持ってない」という謎のメッセージで意味がわからない
        - ![image](https://gyazo.com/2f20a903f83e273c1e655ee01888d130/thumb/1000)
    - OUTPUTタブに具体的にどこでこけたか表示されてる
:

```
    TypeError: Cannot read property 'map' of undefined

      45 |   };
      46 | 
    > 47 |   const NGKW_Buttons = lastKeywords.map((x) => {
```

    - index.tsxで行ってたReactNの初期化が走らないせいだった
    - 同様にSentryの初期化も走ってない
        - これは使ってたところがそもそもAPIアクセスだったのでモックに置き換えた
ts

```typescript
import * as getNewTalkID from "./getNewTalkID";
jest.spyOn(getNewTalkID, "getNewTalkID").mockImplementation(() => {
  getNewTalkID._gotNewTalkID("test");
});
```


- スナップショットの取り方はよくわからない
    - テストの編集によって自動で走った結果「スナップショットを更新するか？」とポップアップが出たのでそれを押した
    - スナップショットテストが通るようになった
    - ![image](https://gyazo.com/2e5d3fa95582b753e2352bf638fc6677/thumb/1000)
    - スナップショットはsrc/__snapshots__/App.test.tsx.snapという名前になった

- KeyPress
    - テキストエリアに対して改行キーのキープレスを送りたかった
ts

```typescript
const textarea = container.querySelector("[id=textarea]");
...
act(() => {
  textarea?.dispatchEvent(
    new KeyboardEvent("keypress", {
      key: "Enter",
      bubbles: true,
    })
  );
});
```

    - 全然反応しない
    - 検索してるとKeyPressではcharCodeを指定しないといけないとか、whichを指定しないといけないとか情報が錯綜している、しかしどちらも指定すると型エラーになる
    - [Test Utilities – React](https://reactjs.org/docs/test-utils.html#simulate)を参考に下記のようにしたら行けた
ts

```typescript
import ReactTestUtils from "react-dom/test-utils";
...
ReactTestUtils.Simulate.keyPress(e, {
  key: "Enter",
});
```


- カバレッジの表示
    - Command Pallete: "Jest: Toggle Coverage Overlay" [doc](https://github.com/jest-community/vscode-jest#coverage)
    - 下記のようなthen節だけあるif文において、then節だけテストで通った場合に「分岐が網羅されてない」という趣旨のハイライトがされる
ts

```typescript
if (props.visible) {
  return ...;
}
return null;
```

    - この時else節をつけてもそれはハイライトされない(え？)
    - 一旦条件式を反転させてみると、当然テストが失敗する
    - その後、元に戻すとハイライトされない(え？)
    - とか色々切り替えて試してたら壊れた笑
        - ![image](https://gyazo.com/5a3eaaaeff76b79d1ab8f7723d2f8693/thumb/1000)
    - vscodeを再起動したらまともな表示に戻ったぞ?
    - ![image](https://gyazo.com/a84a160e59f4fbded5736e83cb8a763d/thumb/1000)
    - もしかしてこれが既にまともではないのか？
    - READMEのどちらの図にも一致しない

- コマンドラインで叩いてみる
    - `$ npm test -- --coverage`
        - うまくいかない
    - `$ npm test -- --coverage --watchAll=false`
        - > react-scripts testはデフォルトで watch モードで Jest を実行するので、watch モードを取り除くためには --watchAll=falseを明示的に指定する必要があります。
            - [Create React App で test coverage が出力されない時の対処 - Qiita](https://qiita.com/nbstsh/items/024391eb1c8ad068d2f6)
            - [https://github.com/facebook/create-react-app/issues/6888](https://github.com/facebook/create-react-app/issues/6888)
    - open `./coverage/lcov-report/index.html`
        - ![image](https://gyazo.com/544a8ffb93ea2d81f7a8ad6c64cb65a4/thumb/1000)
        - ![image](https://gyazo.com/ba313ac952cef099e3351d03f14ff4b4/thumb/1000)

メニューアイコンをクリックして、出てきたメニューをクリックしたい
- ![image](https://gyazo.com/86047ba4bcf1d8f5c93def3897b8fc17/thumb/1000)
- えええ、2回クリックしたらReactFiberのエラー
