---
title: "ReactN"
---

Reactの状態管理を一つのオブジェクトにまとめることでシンプルにする。しばらく使ってるけど便利。
- [Redux不要論と、グローバル状態管理ライブラリReactNの紹介 - Qiita](https://qiita.com/tuttieee/items/e5b2725b3e58cae9ddd6?fbclid=IwAR0PyerLkVqpkGYfnd6EPGt7IVVBXlc3ei5VkWhMutmX8kKzvL4DridbW_4)
- 状態更新に関する[Facebookでの議論](https://www.facebook.com/nishiohirokazu/posts/10220056913269661)

[CharlesStover/reactn: React, but with built-in global state management.](https://github.com/CharlesStover/reactn)
- `$ npm install reactn`

[[ReactN devtool]]
- `$ npm install redux reactn-devtools`
ts

```typescript
import addReactNDevTools from "reactn-devtools";
addReactNDevTools({ trace: true, traceLimit: 25 });
```


TypeScriptと組み合わせて使う場合、型チェックをきちんと働かせるためのコードが必要。
僕は初期値の設定と型の設定をまとめてやるようにしている。
[[initializeGlobalState.ts]]
initializeGlobalState.ts

```typescript
import { setGlobal } from 'reactn';

const INITIAL_GLOBAL_STATE = {
  logs: [] as string[],
}

export const initializeGlobalState = () => {
  setGlobal(INITIAL_GLOBAL_STATE);
}

type TYPE_GLOBAL_STATE = typeof INITIAL_GLOBAL_STATE

declare module 'reactn/default' {
  export interface State extends TYPE_GLOBAL_STATE { }
}
```


index.ts

```typescript
initializeGlobalState()
ReactDOM.render(<App />, document.getElementById('root'));
```


Next.jsではwithInitを使う
- [[Next.jsでReactNを使う]]

---

some.tsx

```
import { useGlobal } from "reactn";
...
// in FC
  // rewrite like below
  // const [logs, setLogs] = useState([] as string[]);
  const [logs, setLogs] = useGlobal("logs");
```


some.tsx

```
somePromise.catch(()=>{
  // rewrite like below
  // setLogs([ERROR_ON_SERVER]);
  // setCanInput(false);
  setGlobal({ logs: [ERROR_ON_SERVER], canInput: false });
})
```



-----
ts

```typescript
import { useGlobal } from 'reactn';

export const PenButton = (props: any) => {
  const [pathCount] = useGlobal("pathCount");
  return <StyledIconButton aria-label="pen">
    <StyledBadge badgeContent={pathCount} color="primary">
      <PenSVGButton onClick={props.onClick} />
    </StyledBadge>
  </StyledIconButton>;
};
```


ts

```typescript
import { getGlobal } from 'reactn';

  tool.onMouseDown = (event: any) => {
    setGlobal({ pathCount: getGlobal().pathCount + 1 })

```



---- ignore below, see [[ReactN+TypeScript]]

ts

```typescript
export const INITIAL_STATE = {
  kanaBuffer: ""
};
export type TState = typeof INITIAL_STATE;
```


tsx

```
import { useGlobal, setGlobal } from 'reactn';
import { INITIAL_STATE, TState } from './INITIAL_STATE';

setGlobal(INITIAL_STATE);

const App: React.FC = () => {
  const [kanaBuffer] = useGlobal<TState>("kanaBuffer");
  return (
      <p>>{kanaBuffer}</p>
      <p>
        <input type="text" onKeyDown={keydownListener}></input>
      </p>
  );
}
```


ts

```typescript
import { getGlobal, setGlobal } from 'reactn';
import { TState } from './INITIAL_STATE';
const kanaListener = (kana: string) => {
  const kanaBuffer = getGlobal<TState>().kanaBuffer;
  setGlobal({ kanaBuffer: kanaBuffer + kana });
}
```







