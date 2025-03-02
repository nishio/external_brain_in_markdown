---
title: "jest.spyOnで差し替わってなかった"
---

jest.spyOnでReact.useStateを差し替える際に`import React, { useState } from "react";`してたせいで差し替わってなかった話

jest.spyOnで処理を差し替えられるのはテストを書く時にとても便利なのだけど、漠然とした「差し替える」ってイメージで使ってると差し替えたつもりで差し代わってないのでモジュールの仕組みをきちんと理解する必要がある


現象を再現するための短いコード
MyComponent.tsx

```
import React, { useState } from "react";

export let setValue: React.Dispatch<React.SetStateAction<string>>;
export const MyComponent = () => {
  const [value, _setValue] = useState("foo");
  setValue = _setValue;
  return <span>{value}</span>;
};
```


Foo.test.tsx

```
import React from "react";
import { MyComponent, setValue } from "./MyComponent";
import { render, screen } from "@testing-library/react";

test("foo", () => {
  render(<MyComponent />);
  screen.getByText("foo");
  setValue("bar");
  screen.getByText("bar");
});
```


この時、[[jest-electron]]を使っているとターミナル上では問題なくテストが通ったように見えるが、実はelectronのコンソールでは警告が出ている
- Terminal on VSCode
    - `$ DEBUG_MODE=1 npm test -- Foo`
    - ![image](https://gyazo.com/98f7d6dc79ae9cb6b30e444b705f1285/thumb/1000)
- Electron
    - ![image](https://gyazo.com/e60b0c9ba51f447e8bb6a4cfd6350dbb/thumb/1000)

で、このReactの状態更新をactで包まないといけない問題を、useStateをモックで差し替えることで実現した
see: [[useStateを差し替える]]

しかしこのケースで、警告は消えない。(実際にこれに気づいた時は、もっと大きくて複雑なシステムのテストをしていて、今までこの方法で警告が消えたケースあったのに、一部のケースだけ消えてない、と気づいた)

何がいけないか？jest.spyOnでuseStateを差し替えたつもりが、差し変わる前のuseStateを使ってしまっている。

まずここでMyComponent.tsxが読まれる
Foo.test.tsx

```
import React from "react";
import { MyComponent, setValue } from "./MyComponent";  // HERE
import { render, screen } from "@testing-library/react";
import { mockUseState } from "./mockUseState";

test("foo", () => {
  const m = mockUseState();
  render(<MyComponent />);
  screen.getByText("foo");
  setValue("bar");
  screen.getByText("bar");
  m.mockRestore();
});
```


次に`(1)`で、MyComponentのスコープにuseStateへの参照が複製される。
MyComponent.tsx

```
import React, { useState } from "react";  // (1)

export let setValue: React.Dispatch<React.SetStateAction<string>>;
export const MyComponent = () => {
  const [value, _setValue] = useState("foo");  // (3)
  setValue = _setValue;
  return <span>{value}</span>;
};
```

MyComponentはこの参照を使ってuseStateを呼び出す。
この後でjest.spyOnでuseStateを差し替える`(2)`が、タイミングが遅い。MyComponentのuseStateは差し替え前のオブジェクトを指したままなので、呼び出し時に差し替えた新しい実装が呼ばれない。

![image](https://gyazo.com/4fed78d8022f240dcf8d20248f9c7c69/thumb/1000)

この問題を解決する手軽な方法は、`useState`ではなく`React.useState`で呼び出すこと。

MyComponent.tsx

```
import React from "react";  // HERE

export let setValue: React.Dispatch<React.SetStateAction<string>>;
export const MyComponent = () => {
  const [value, _setValue] = React.useState("foo");  // HERE
  setValue = _setValue;
  return <span>{value}</span>;
};
```


これなら呼び出しのタイミングで、React.setStateが指す値を解決するので、差し替えた新しい実装が呼ばれる。
![image](https://gyazo.com/4fed78d8022f240dcf8d20248f9c7c69/thumb/1000)

なおこういうミスを未然に防ぐためにもっと早い段階で実装の差し替えをする案がある。jest.mockで差し替えるとJestによる実行順序の変更でimportより先にJestのモック関数に差し代わる。その上で実装差し替えメソッドを呼べば参照が変わらないまま実装が変わる。
