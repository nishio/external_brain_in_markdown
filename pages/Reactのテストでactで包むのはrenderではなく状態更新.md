---
title: "Reactのテストでactで包むのはrenderではなく状態更新"
---

[[Jest]] + [[React Testing Library]] で Reactで書かれたコンポーネントをテストするにあたって非同期の状態更新やレンダリングの振る舞いがわかりにくかったので小さいサンプルを作って確認した。

まず、Reactの`useState`で値を持って、それを表示するだけのコンポーネントを作る。
`props.exportSetValue`は`setValue`をテストコードの側に露出させるためのコールバック。
MyComponent.tsx

```
import { useState } from "react";

export const MyComponent = (props: {
  exportSetValue: (
    setValue: React.Dispatch<React.SetStateAction<number>>
  ) => void;
}) => {
  const [value, setValue] = useState(0);
  props.exportSetValue(setValue);
  return <span>{value}</span>;
};
```


成功するテストケース1。冒頭の5行は`setValue`を取り出すためのもの。
テストシナリオは「レンダリングして、0が表示されてることを確認し、`setValue(1)`して、1が表示されていることを確認する」というもの。
注目するところは、(1)の`render`が`act`でラップされておらず、 (2)の`setValue`が`act`でラップされているところ。
test.ts

```typescript
test("MyComponent1", () => {
  type TSetState = React.Dispatch<React.SetStateAction<number>>;
  let setValue: TSetState | undefined;
  const exportSetValue = (s: TSetState) => {
    setValue = s;
  };

  render(<MyComponent exportSetValue={exportSetValue} />);  // (1)
  expect(screen.getByText("0")).toBeTruthy();
  expect(setValue).toBeTruthy();
  act(() => {
    setValue!(1);  // (2)
  });
  expect(screen.queryByText("0")).toBeNull();
  expect(screen.getByText("1")).toBeTruthy();
});
```


[act()](https://ja.reactjs.org/docs/testing-recipes.html#act)の解説には下記のようなサンプルコードが書いてあるが、ものすごくミスリーディング。
sample.ts

```typescript
act(() => {
  // render components
});
// make assertions
```

解説文章を読むと一応ユーザイベントもレンダーもユニットである、とは書いてある。
- > UI テストを記述する際、レンダー、ユーザイベント、データの取得といったタスクはユーザインターフェースへのインタラクションの「ユニット (unit)」であると考えることができます。react-dom/test-utils が提供する act() というヘルパーは、あなたが何らかのアサーションを行う前に、これらの「ユニット」に関連する更新がすべて処理され、DOM に反映されていることを保証します。

`setValue`が`act`でラップされていない場合に出る警告はもっとまともなことが書いてある。
- > When testing, code that causes React state updates should be wrapped into act(...)
    - 「Reactの状態更新を引き起こすコードは`act`でラップせよ」
    - 今回の例でなぜ`render`をラップしないで良いかというと、それが状態更新を引き起こさないからだ
    - この警告メッセージに含まれるサンプルコードではactの中身のコメントが`// render components`ではなく`/* fire events that update state */`になっている
        - ドキュメントの側もこちらにあわせるべきでは？

full warning:
output

```
Warning: An update to MyComponent inside a test was not wrapped in act(...).
    
    When testing, code that causes React state updates should be wrapped into act(...):
    
    act(() => {
      /* fire events that update state */
    });
    /* assert on the output */
    
    This ensures that you're testing the behavior the user would see in the browser. Learn more at https://reactjs.org/link/wrap-tests-with-act
        at MyComponent (/Users/nishio/keicho-webclient/src/MyComponent.tsx:8:29)

      52 |   // act(() => {
    > 53 |   setValue!(1);
         |   ^
```


ここから本題になるのだけど別のページに分ける
[[Promiseの結果で状態更新する場合、全体をactで包んでもダメ]]