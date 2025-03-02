
3行で言えば
- コンポーネントのマウントの前に1回だけグローバル状態の初期化をしたい
- しかし[[Next.js]]ではそれを手軽に書ける場所がない
- ので、1回だけ初期化を実行する高階コンポーネント([[HOC]])を使って初期化を行う。
> In some cases (such as when using [[Next.js]]), you may be unable to run a setup script prior to your ReactN components mounting. In order to instantiate your global state and reducers prior to mounting, you may use the withInit Higher Order Component. This HOC will await the setting of your global state before mounting the provided Lower Order Component (e.g. <App />).
[https://github.com/CharlesStover/reactn#withinit](https://github.com/CharlesStover/reactn#withinit)

Next.jsのコードジェネレータが作ったコード`_app.tsx`はこんな感じ
_app.tsx

```
import '../styles/globals.css'
import type { AppProps } from 'next/app'

function MyApp({ Component, pageProps }: AppProps) {
  return <Component {...pageProps} />
}

export default MyApp
```


これに高階コンポーネントwithInitをつける。
READMEのサンプルは下記のようになっているが
- 型情報がない
- コンポーネントが引数を取らない
という点でそのまま`_app.tsx`に適用できない。
ts

```typescript
import React, { useDispatch, useGlobal, withInit } from 'reactn';

const INITIAL_REDUCERS = {
  addOne: ({ count }) => ({
    count: count + 1,
  }),
};

const INITIAL_STATE = {
  count: 0,
};

export default withInit(
  INITIAL_STATE,
  INITIAL_REDUCERS
)(function App() {
  const addOne = useDispatch('addOne');
  const [count] = useGlobal('count');
  return <button onClick={addOne}>Count: {count}</button>;
});
```


ソースを読んで確認したけども、3番目の型引数でコンポーネントの引数の型を受け取っていた。なのでそこに適切に渡してやればOK。
TypeScriptで使うときのためのdeclareもする。
- [https://github.com/CharlesStover/reactn#typescript-support](https://github.com/CharlesStover/reactn#typescript-support)

_app.tsx

```
import "../styles/globals.css";
import type { AppProps } from "next/app";
import React, { withInit } from "reactn";

const INITIAL_STATE = {
  count: 0,
};

type TYPE_STATE = typeof INITIAL_STATE;

const INITIAL_REDUCERS = {
  addOne: ({ count }: TYPE_STATE) => ({
    count: count + 1,
  }),
};

type TYPE_REDUCERS = typeof INITIAL_REDUCERS;

declare module "reactn/default" {
  export interface State extends TYPE_STATE {}
  export interface Reducers extends TYPE_REDUCERS {}
}

const MyApp = withInit<TYPE_STATE, TYPE_REDUCERS, AppProps>(
  INITIAL_STATE,
  INITIAL_REDUCERS
)(({ Component, pageProps }: AppProps) => {
  return <Component {...pageProps} />;
});

export default MyApp;
```


