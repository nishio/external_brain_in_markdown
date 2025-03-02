---
title: "変更差分を作ってsetGlobalする"
---

[[ReactNのuseGlobalは参照が変化しなくても発火しうる]]ということが発覚した。
つまりオブジェクト全体をsetGlobalに渡してしまうとすべてのフックが発動して再描画されてしまう。
どう対処しようかしばらく考えて、オブジェクト全体を渡すのはimmerで全体のdraftを作って破壊的更新をしている場合だと気づいたので、そのための自作ユーティリティ関数updateGlobalを「変更差分を作って更新する」という仕組みに変えた

before
ts

```typescript
import { State } from "reactn/default";
import { setGlobal } from "reactn";
import { produce } from "immer";

export const updateGlobal = (update: (g: State) => void) => {
  // update global variable in destructive manner using immer
  setGlobal((g: State) => {
    return produce(g, update);
  });
};
```


after
ts

```typescript
import { State } from "reactn/default";
import { setGlobal } from "reactn";
import { produce } from "immer";

export const updateGlobal = (update: (draft: State) => void) => {
  // update global variable in destructive manner using immer
  setGlobal((current_state: State) => {
    const new_state = produce(current_state, update);
    const update_delta: { [key: string]: unknown } = {};
    Object.entries(current_state).forEach(([key, ref]) => {
      // @ts-ignore
      if (current_state[key] !== new_state[key]) {
        // @ts-ignore
        update_delta[key] = new_state[key];
      }
    });
    return update_delta;
  });
};
```


before / after
![image](https://gyazo.com/8daea14561c18aa4c85a9e22d8905b5e/thumb/1000)![image](https://gyazo.com/2378a32ec9295a85dff707a096f7615a/thumb/1000)
単なるmousedownで画面全体を再描画して120msかかってたのが必要な部分だけの4.8msになった、めでたしめでたし
