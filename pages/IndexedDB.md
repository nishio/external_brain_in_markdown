
> IndexedDB API is powerful, but may seem too complicated for simple cases. If you'd prefer a simple API, try libraries such as localForage, dexie.js, ... that make IndexedDB more programmer-friendly.
- [IndexedDB API - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)

- [[Dexie.js]]
    - A Minimalistic Wrapper for IndexedDB
    - [https://dexie.org/](https://dexie.org/)
- `$ npm install dexie`
- Read [Typescript](https://dexie.org/docs/Typescript)
    - 型の都合でクラスを定義する必要がある
    - `// (1)`で指定した名前はブラウザのスコープで露出するので人間可読なアプリ名称などを入れてわかりやすくする
localDB.ts

```typescript
import Dexie from "dexie";

export interface ITalks {
  id?: number; // Primary key. Optional (autoincremented)
  TalkID: string;
}
class MyAppDatabase extends Dexie {
  talks: Dexie.Table<ITalks, number>; // number = type of the primkey

  constructor() {
    super("MyAppDatabase");  // (1)
    this.version(1).stores({
      talks: "++id",
    });
    this.talks = this.table("talks");
  }
}

export const localDB = new MyAppDatabase();
```

use.ts

```typescript
localDB.talks
  .orderBy("id")
  .reverse()
  .limit(1)
  .toArray()
  .then((x) => {
    setGlobal({ TalkID: newID, previousTalkID: x[0].TalkID });
    localDB.talks.add({ TalkID: newID });
  });
```


- Chrome Dev Tool > Applicationで内容を見れる
    - ![image](https://gyazo.com/1b6ecf332579b1e48810e84fe64bff38/thumb/1000)

