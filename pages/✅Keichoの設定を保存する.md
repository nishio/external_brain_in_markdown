
- Scrapbox
    - ユーザアイコンを覚える
    - プロジェクト名を覚える

- 将来的にはユーザの好むスクロール位置とかも?

Config.ts

```typescript
import { getGlobal, setGlobal } from "reactn";
import { localDB } from "./localDB";

export const defaultConfig = {
  ...
};

const load = () => {
  return localDB.config
    .get(1)
    .then((config) => {
      if (config === undefined) {
        return defaultConfig;
      }
      return { ...defaultConfig, ...JSON.parse(config.json) };
    })
    .then((config) => {
      setGlobal({ config });
    });
};

const save = () => {
  const json = JSON.stringify(getGlobal().config);
  localDB.config.put({ json }, 1);
};

const Config = { load, save };
export default Config;
```


index.tsx

```
import Config from "./Config";
Config.load();
```


initializeGlobalState.ts

```typescript
import { defaultConfig } from "./Config";
const INITIAL_GLOBAL_STATE = {
  ...
  config: defaultConfig,
};
```

[[initializeGlobalState.ts]]

localDB.ts

```typescript
import Dexie from "dexie";
export interface IConfig {
  id?: number; // Primary key. Optional (autoincremented)
  json: string;
}
class MyAppDatabase extends Dexie {
  // Declare implicit table properties.
  // (just to inform Typescript. Instanciated by Dexie in stores() method)
  talks: Dexie.Table<ITalks, number>; // number = type of the primkey
  config: Dexie.Table<IConfig, number>;
  //...other tables goes here...

  constructor() {
    super("Keicho");
    this.version(4).stores({
      talks: "++id,TalkID,last_modified",
      config: "++id,json",
      //...other tables goes here...
    });
    // The following line is needed if your typescript
    // is compiled using babel instead of tsc:
    this.talks = this.table("talks");
    this.config = this.table("config");
  }
}
```


ScrapboxDialog.tsx

```
export const ScrapboxDialog = () => {
  ...
  const [g] = useGlobal();
  ...
  const projectName = g.config.project_name;
  ...
  const handleClose = () => {
    Config.save();
    setDialog(null);
  };
  ...
  const onChangeProjectName = (e: React.ChangeEvent<HTMLInputElement>) => {
    updateGlobal((g) => {
      g.config.project_name = e.target.value;
    });
  };
  ...
  return (...
          <label>Project Name: </label>
          <input
            type="text"
            defaultValue={projectName}
            onChange={onChangeProjectName}
          ></input>
          ...
  );
};
```


状態の更新には[[immer]]を使っている
[[updateGlobal.ts]]
