
ここまでの話:
- 1: [[Reactのテストでactで包むのはrenderではなく状態更新]]
- 2: [[Promiseの結果で状態更新する場合、全体をactで包んでもダメ]]

ユーザの発生させるイベントによって新しいPromiseが作成され、そのthenでReactの状態更新が行われるようなコードをJestでテストしたい。
- 例えば「ユーザがボタンをクリックするとネットワークアクセスをして、結果を描画」などがこのケースに当てはまる。
- ネットワークアクセスの部分をモックで置き換えたとしてもPromiseによって非同期になることは変わらない。

このようなシチュエーションで「waitForで期待するエレメントが出現するまで待つ」というアプローチが知られているが、このアプローチだと「ネットワークのレスポンスがAだったらメニューを表示、Bだったら出さない」などの場合にBの側のテストができない。状態更新による再描画の完了を知る方法が必要。

シンプルなコンポーネントを使って試す。`userTrigger`はPromiseを使って返す。(これは伏線)
ts

```typescript
import { useState } from "react";
export type TUserTrigger = () => void;
export type TResolve = (value: number) => void;
export let userTrigger: TUserTrigger;
export let resolve: TResolve;

export const MyAsyncComponent = () => {
  const [value, setValue] = useState(0);
  userTrigger = () => {
    return new Promise<number>((res) => {
      resolve = res;
    }).then((x) => {
      setValue(x);
    });
  };
  return <span>{value}</span>;
};
```


テストシナリオは「初回描画時は0、ユーザがトリガーした直後も0、Promiseがresolveされたら1」というもの。
下記の書き方ではfailする。
ts

```typescript
test("MyAsyncComponent1", async () => {
  render(<MyAsyncComponent />);
  expect(screen.getByText("0")).toBeTruthy();

  userTrigger();
  expect(screen.getByText("0")).toBeTruthy();

  resolve(1);
  expect(screen.queryByText("0")).toBeNull(); // fails
  expect(screen.getByText("1")).toBeTruthy();
});
```


resolveの後のthenの実行は必ず非同期だから、その下の行がthenの実行より後に実行されることを保証するには、作られたPromiseにthenでつなげたり、awaitしたりするしかない。
(以前ここに[[非同期たまたま動いたけど不適切]]な例が書いてあったので、別ページに移動した)

下記の書き方で、(1)で行ったユーザ操作によって引き起こされた非同期な更新が完了した後の状態を(2)でテストできる
ts

```typescript
test("MyAsyncComponent1", async () => {
  ...
  render(<MyAsyncComponent />); 
  ...
  const p: Promise<unknown> = userTrigger();  // (1)
  ...	
  resolve(1);
  ...
  await p;
  ... // (2)
});
```


setValueでの更新をactで包むために[[useStateを差し替える]]
下記のコードで、console.logが1〜11まで順番通りに出た後、2〜4、つまり「コンポーネントの再描画」が走って、その後で12が表示される。
MyAsyncComponent.tsx

```
import { useState } from "react";
export type TUserTrigger = () => Promise<unknown>;
export type TResolve = (value: number) => void;
export let userTrigger: TUserTrigger;
export let resolve: TResolve;

export const MyAsyncComponent = () => {
  console.log(2);
  const [value, setValue] = useState(0);
  console.log(4);
  userTrigger = () => {
    console.log(6);
    return new Promise<number>((res) => {
      console.log(7);
      resolve = res;
    }).then((x) => {
      console.log(10);
      setValue(x);
    });
  };
  return <span>{value}</span>;
};
```

My.test.ts

```typescript
import React, { Dispatch } from "react";
import { act, render, screen } from "@testing-library/react";

import { MyAsyncComponent, resolve, userTrigger } from "./MyAsyncComponent";
import { useState as originalUseState } from "react";

test("MyAsyncComponent1", async () => {
  jest.spyOn(React, "useState").mockImplementation((arg?: unknown): [
    unknown,
    Dispatch<unknown>
  ] => {
    console.log(3);
    const [s, setS] = originalUseState(arg);
    return [
      s,
      (arg: unknown) => {
        console.log(11);
        act(() => {
          setS(arg);
        });
      },
    ];
  });
  console.log(1);
  render(<MyAsyncComponent />);
  console.log(5);
  expect(screen.getByText("0")).toBeTruthy();

  const p: Promise<unknown> = userTrigger();
  console.log(8);
  expect(screen.getByText("0")).toBeTruthy();

  resolve(1);
  console.log(9);
  expect(screen.getByText("0")).toBeTruthy();

  await p;
  console.log(12);
  expect(screen.getByText("1")).toBeTruthy();
});
```


さて、これで処理の流れを期待通りにコントロールできるようになった。めでたしめでたし、と終わるつもりだったが…
> `userTrigger`はPromiseを使って返す。(これは伏線)

イベントハンドラやuseEffectの中でPromiseを作る場合、そのPromiseを返り値としてテストコードに返すことができない。
- useEffectは「返り値はcleanup関数」と定めている [doc](https://reactjs.org/docs/hooks-effect.html#example-using-hooks-1)
- `fireEvent.click`は`(element: ...) => boolean`

選択肢は2つ思いつく
- 作られたPromise自体をexport
- Promiseを作る部分を関数に切り出してexportし、それをjestでmockして返り値を抜き取る

僕は後者がめんどくさいので前者でやるが、好みが分かれるところだと思う
次回: [[useEffectで作ったPromiseをexport]]
