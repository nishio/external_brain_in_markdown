
[[TypeScript]]での辞書的オブジェクトの扱いがわからなくて試行錯誤した。
まずJavaScriptのMapとObjectを正しく区別することが大事
- [Map - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- MapとObjectはどちらもKey-Valueの辞書的振る舞いをする
- 特にPythonistaにとって混乱しやすい
    - Pythonでは`{}`が辞書。
    - JavaScriptでは`{}`がObject
    - JavaScriptの`{}`はPythonでは`object`
- JavaScriptのMapの場合
    - `const aMap = new Map<string, number>();`
    - `aMap.set("a", 1);`
    - `aMap.forEach((value: number, key: string) => {});`
- Objectの場合
    - `const obj = {} as { [key: string]: number };`
    - `obj["a"] = 1` or  `obj.a = 1`
    - `Object.entries(obj).forEach(([key, value]) => {})`

ts

```typescript
  const aMap = new Map<string, number>();
  if (aMap.get("a") === undefined) {
    aMap.set("a", 1);
  }
  aMap.forEach((value: number, key: string) => {
    console.log(key, value);
  });

  const obj = {} as { [key: string]: number };
  if (obj["a"] === undefined) {
    obj["a"] = 1;
  }
  Object.entries(obj).forEach(([key, value]) => {
    console.log(key, value);
  });
```


-----試行錯誤
ts

```typescript
Array.from(preset_tests.entries()).map(
   ([key, value]: [string, any]) => <li><a href={"#" + key}>{key}: {value.title}</a></li>
 );
```



Object.entries(map)
[[TypeScript]]
ts

```typescript
// const map: Map<string, {
//   data: string;
//   title: string;
// }>
const x = Object.entries(map);
// const x: [string, any][]
const y = map.entries;
// const y: () => IterableIterator<[string, {
//   data: string;
//   title: string;
// }]>
```

