
良いやり方かどうかはさておき、手順をメモしておく

- 選択範囲をJSONに吐き出す実装をしたい
- 対話的に色々試してからどう実装するか決めたい
- 選択範囲はどこにあるか？
    - `const App = (props: any) => {...}`の中で
        - `let [selection, setSelection] = useState<PaperItem[]>([]);`
    - 関数のローカルスコープなので露出してない
    - `window.debug.selection = selection;`で露出させる
        - 関連: [[TypeScriptでwindowに新しいプロパティを足す]]
        - いちいち宣言しなくても良いように型をanyにしたwindow.debugを用意してある
        - @ts-ignoreでもいい
- オブジェクトをプレーンなオブジェクトに変換するコードはどこにあるか
    - `const stateItemToFirestore = (x: StateItem) => {...}`
    - これも関数定義の後で`window.debug.stateItemToFirestore = stateItemToFirestore`...
        - しようと思ったがNG
            - window.debugを作るコードよりもこの関数定義のコードの方が先に走るため
    - `export stateItemToFirestore`する
        - window.debugを作っているコードの側で、それをimportして露出させる
    - [[オブジェクトを露出させる方法に関する考察]]
- 続き
    - `window.debug.stateItemToFirestore(window.debug.selection)`
        - エラー
    - `window.debug.stateItemToFirestore(window.debug.selection[0])`
        - エラー
    - `window.debug.stateItemToFirestore(window.debug.selection[0]).item`
        - OK
    - これは呼び出す時に引数の型を間違えている
        - TypeScriptとして記述してたら型エラーで理由がわかった？
        - →NO、`window.debug:any`に入れた時点で型情報は失われている
    - `JSON.stringify(...)`
        - 目的の文字列が得られた
    - 次はこれをMapに戻す方法を考える
- `updateStateItem`がexportされているのでそれを露出する
    - →単純に読んでエラー
- `firestoreToStateItem`が必要
    - できた
    - ![image](https://gyazo.com/5eb6bca96b3a751c15a074ec1a180cfc/thumb/1000)
- TypeScriptのコードにする
ts

```typescript
export const exportSelectedItemsAsJSON = () => {
  const r = selectedItems.map((x) =>
    stateItemToFirestore(x.item)
  );
  return JSON.stringify(r);
};

export const importItemsFromJSON = (json: string) => {
  const xs = JSON.parse(json);
  xs.forEach((x: object) => {
    updateStateItem(null, firestoreToStateItem(x))
  })
};
```

- これで期待通りに動く: `debug.importItemsFromJSON(debug.exportSelectedItemsAsJSON())`
- でも`debug.exportSelectedItemsAsJSON()`でコンソールに表示されたJSONをコピペしても壊れてしまう
    - まあ開発者コンソールでJSONが正しくパースされなくても仕方ない
- `localStorage["tmp"] = debug.exportSelectedItemsAsJSON()`
- 別ウィンドウで`debug.importItemsFromJSON(localStorage["tmp"])`
- 正しく動いた
