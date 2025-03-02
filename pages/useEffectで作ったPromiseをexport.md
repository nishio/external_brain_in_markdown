
Promiseによって非同期で行われる状態更新の結果をテストしたい。
前回の話: [[非同期なReactの状態更新をテストする]]で、Promiseを返り値として得られる場合の解説をした。
useEffectは返り値がcleanup関数と定められているのでその方法は使えない。そこで作られたPromiseをexportすることにした。

シンプルに下記のコードで目的が達成できる。
なおloadFromServerはサーバからfetchするコードがモック実装で置き換えられたものとする。
promiseの型は`Promise<unknown>`で構わない。テストコード内でawaitするのにしか使わないので。
MyUseEffectComponent.tsx

```
import { useEffect, useState } from "react";
export let promise: Promise<unknown>;

const loadFromServer = async () => 1;

export const MyUseEffectComponent = () => {
  const [value, setValue] = useState(0);
  useEffect(() => {
    promise = loadFromServer().then((x) => {
      setValue(x);
    });
  }, []);
  return <span>{value}</span>;
};
```


テストコード。
冒頭の[[useStateを差し替える]]はここでは解説しない。
My.test.ts

```typescript
test("MyUseEffectComponent", async () => {
  jest.spyOn(React, "useState")...;

  render(<MyUseEffectComponent />);
  expect(screen.getByText("0")).toBeTruthy();

  await promise;
  expect(screen.getByText("1")).toBeTruthy();
});
```

