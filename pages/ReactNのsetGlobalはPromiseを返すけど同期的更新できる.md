
ReactNのsetGlobalは`Promise<G>`を返すので、てっきり「非同期にいつだかわからないタイミングで更新され、Promiseのthenが呼ばれる」と思っていた。
なので順番に呼ばれることを保証するためにはasync/awaitしなきゃいけないと思っていた。

これは間違い。
引数newGlobalStateがプロミスである場合以外は同期的に更新してからresolve済みのPromiseを返す。

ts

```typescript
export default function _setGlobal<...>(
  globalStateManager: GlobalStateManager<G, R>,
  newGlobalState: NewGlobalState<G>,
  callback: Callback<G, R> = null,
): Promise<G> { ... }
```

[https://github.com/CharlesStover/reactn/blob/master/src/set-global.ts](https://github.com/CharlesStover/reactn/blob/master/src/set-global.ts)
第一引数にデフォルトのGlobalStateManagerをbindしている
- `setGlobal: setGlobal.bind(null, defaultGlobalStateManager),` [index.ts](https://github.com/CharlesStover/reactn/blob/master/src/index.ts)

引数がPromiseでない場合は最終的にここにくる
ts

```typescript
  public setObject<O extends Partial<G> = Partial<G>>(
    obj: O, ...
  ): Promise<Partial<G>> {
    ...
    const stateChange: Partial<G> = this.flush(reducerName, reducerArgs);
    return Promise.resolve(stateChange);
  } 
```

[https://github.com/CharlesStover/reactn/blob/master/src/global-state-manager.ts#L350](https://github.com/CharlesStover/reactn/blob/master/src/global-state-manager.ts#L350)

引数がPromiseの場合は与えられたPromiseのthenにつながる
ts

```typescript
  public setPromise(
    promise: Promise<NewGlobalState<G>>, ...
  ): Promise<Partial<G>> {
    return promise
      .then((result: NewGlobalState<G>): Promise<Partial<G>> =>
        this.set(result, reducerName, reducerArgs),
      );
  }
```

