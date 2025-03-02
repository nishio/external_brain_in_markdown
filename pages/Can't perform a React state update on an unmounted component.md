
from [[Jestメモ]]
Can't perform a React state update on an unmounted component
2021-03-09
- > Warning: Can't perform a React state update on an unmounted component. This is a no-op, but it indicates a memory leak in your application. To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
- まとめてテストした時に、コンポーネントがアンマウントされてから状態更新して警告される場合があり、それは非同期の更新が完了するのを待たずにテストケースが終了してしまってると思われる
2021-03-11
- イベントハンドラからasyncを無くす作業をしたのにアンマウント後の更新が起きる問題が解決しなくてよくわからなくなっている
2021-03-12
- [React state update on an unmounted component | Code, Thoughts & Opinions - By Sagiv Ben Giat](https://www.debuggr.io/react-update-unmounted-component/)
    - 同じ問題を再現するサンプルコードを見たりしたけどにてるところをコメントアウトしても再現するのでこれは今再現してるコードから削っていって最小限の再現コードを作るしかないな、というのをやってるのだが全く予想外のものが影響してて、なんだろうなとなってる
    - ワークアラウンドと、なぜここでだけ発生するのかががわかったけど問題が発生する原理がよくわからないなぁ
        - ワークアラウンド: `useGlobal()`を`useGlobal("foo")`にする
- 「なるほどReactNの中でuseEffectのクリーンアップをしてないに違いない！」と思ってソースを読んだらやっていた…
    - モック絡みでクリーンアップがうまくいってないのかな…
- とりあえずわかったこと
    - 非同期更新のせいでアンマウント後に更新が遅れてるのではない
    - 次のテストケースの開始時に値を初期化するところでアンマウント後のコンポーネントが更新されようとしている
        - テスト環境でしか起こらないし、警告が出るだけで処理に影響はない
        - 複数のテストケースを実行した時にだけ起こるのはこれが原因
- これを防ぐためにuseEffectのクリーンアップでフラグを立ててそれ以上更新されないようにする方法が知られている
    - [React state update on an unmounted component | Code, Thoughts & Opinions - By Sagiv Ben Giat](https://www.debuggr.io/react-update-unmounted-component/)
    - ReactNは内部的にuseEffectを使っている
    - しかしクリーンアップもやっている
- ReactNの実装でクリーンアップ自体は呼ばれてる！
- 読んだ結果を描画に使ってなくても警告が再現するのは、getterを監視しているから
    - [[ReactNのuseGlobalはgetを監視する]]
ts

```typescript
// Happen
const [g] = useGlobal()
console.log(g.foo);
return null;
// Not Happen
const [g] = useGlobal()
return null;
```

- 更新リスナーがなぜか二つついている、これは正しい挙動か？
- setGlobalでなぜか更新リスナーが追加される
    - コードの目的としてここで追加される意味がわからないし
    - コードを読んでも何故追加が起きているのかわからない
    - そしてこのリスナーはコンポーネントのアンマウント時に解除されないのでテストケースを跨いでリークする
- setGlobalでコンポーネントの再描画がトリガーされる
    - 再描画でget監視し、再び更新リスナーの追加が走る
    - この時リスナーが同一なので追加しても増えないのが期待される挙動
    - 実際には同一でないので追加で増える
    - クリーンアップで最後の一つしか削除されない
- ReactN自体のテストコードでは確かにリスナーが同一である
    - つまり僕がやったことが原因でリスナーの同一性が失われてる
- MockUseStateを止めると(actの警告は出るが)この警告は出なくなる
- 更新リスナーは[[use-force-update]]である
    - [https://github.com/CharlesStover/use-force-update/blob/master/src/use-force-update.ts](https://github.com/CharlesStover/use-force-update/blob/master/src/use-force-update.ts)
use-force-update.ts

```typescript
import { useCallback, useState } from 'react';

// Returning a new object reference guarantees that a before-and-after
//   equivalence check will always be false, resulting in a re-render, even
//   when multiple calls to forceUpdate are batched.

export default function useForceUpdate(): () => void {
  const [ , dispatch ] = useState<{}>(Object.create(null));

  // Turn dispatch(required_parameter) into dispatch().
  const memoizedDispatch = useCallback(
    (): void => {
      dispatch(Object.create(null));
    },
    [ dispatch ],
  );
  return memoizedDispatch;
}
```

    - これはuseStateの第二返り値をuseCallbackしたものを返す
- [doc](https://reactjs.org/docs/hooks-reference.html)
    - > React guarantees that setState function identity is stable and won’t change on re-renders. This is why it’s safe to omit from the useEffect or useCallback dependency list.
    - > [[useCallback]] will return a memoized version of the callback that only changes if one of the dependencies has changed.
    - つまり何度呼び出されても同一であることが保証されてる
- 一方僕のコード
MockUseState.ts

```typescript
import React, { Dispatch } from "react";
import { act } from "@testing-library/react";
import { useState as originalUseState } from "react";

export const mockUseState = () => {
  return jest.spyOn(React, "useState").mockImplementation((arg?: unknown): [
    unknown,
    Dispatch<unknown>
  ] => {
    const [s, setS] = originalUseState(arg);
    return [
      s,
      (arg: unknown) => {
        act(() => {
          setS(arg);
        });
      },
    ];
  });
};
```

    - なるほど、これは呼び出しのたびに違うものを返しそうだ
    - use-force-updateと同じように[[useCallback]]しよう
ts

```typescript
export const mockUseState = () => {
  return jest.spyOn(React, "useState").mockImplementation((arg?: unknown): [
    unknown,
    Dispatch<unknown>
  ] => {
    const [s, dispatch] = originalUseState(arg);
    const wrappedDispatch = useCallback(
      (arg: unknown): void => {
        act(() => {
          dispatch(arg);
        });
      },
      [dispatch]
    );
    return [s, wrappedDispatch];
  });
};
```

- やったー、ついに警告なくテストが通ったぞ！
