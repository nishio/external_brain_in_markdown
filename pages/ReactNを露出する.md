
2021-06-28
- グローバルな値を自分で管理する必要はない、ReactNに任せれば良い
- 値の読み書きのためのインターフェイスだけ露出すれば良い

以前の議論
- [[TypeScriptでwindowに新しいプロパティを足す]]
- [[オブジェクトを露出させる方法に関する考察]]

ts

```typescript
import { getGlobal, setGlobal } from "reactn";

const movidea = {
  setGlobal,
  getGlobal,
};

const debug = {};

declare global {
  interface Window {
    debug: any;
    movidea: typeof movidea;
  }
}

export const initializeGlobalVariables = () => {
  window.movidea = movidea;
  window.debug = debug;
};
```


