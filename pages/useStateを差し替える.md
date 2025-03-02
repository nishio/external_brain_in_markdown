---
title: "useStateを差し替える"
---

from [[非同期なReactの状態更新をテストする]]
useStateを差し替える

コンポーネントの中でsetValueしている場合に、これがactで包まれていないと警告される
- 関連: [[Reactのテストでactで包むのはrenderではなく状態更新]]

output

```
console.error
    Warning: An update to MyAsyncComponent inside a test was not wrapped in act(...).
    When testing, code that causes React state updates should be wrapped into act(...):
...
      15 |       console.log(6);
    > 16 |       setValue(x);
         |       ^
```


簡単な解決策としては「何もしないact実装を用意して本体コード中でそれを使っておき、テストの時だけ本物に差し替える」という案もあるが、なんとなく嫌なので useStateを差し替える。

MockUseState.ts

```typescript
import React, { Dispatch, useCallback } from "react";
import { act } from "@testing-library/react";
import { useState as originalUseState } from "react";

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

updated 2021-03-12

test.tsx

```
let m_mockUseState: jest.SpyInstance<[unknown, React.Dispatch<unknown>], []>;
beforeEach(() => {
  m_mockUseState = mockUseState();
});
afterEach(() => {
  m_mockUseState.mockRestore();
}); 
```

