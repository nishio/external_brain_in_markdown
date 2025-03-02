---
title: "Jestのモックは同一モジュール内の呼び出しに影響を与えない"
---

from [[Jestメモ]]
[[Jest]]のモックは同一モジュール内の呼び出しに影響を与えない
MyModule.ts

```typescript
export const A = () => "old value";
export const callA = () => A();
```

test.ts

```typescript
test("render", () => {
  jest.spyOn(MyModule, "A").mockImplementation(() => {
    return "new value";
  });
  expect(MyModule.callA()).toBe("new value");
```

result

```
Error: expect(received).toBe(expected) // Object.is equality

Expected: "new value"
Received: "old value"
```


モジュールの中の特定の関数だけ1行で別の処理に置き換えることができるのは便利だが、それが同一モジュール内の関数から呼ばれてる場合は混乱の元になる
Aをモックに置き換えるのが本当に正しい場合、callAとAの間にモジュール境界があるべき(OK1)だし、callAとAを別のモジュールに分けるのが適当でないくらい密結合なのであればモックに置き換えるべきなのはAではない(OK2)、ということか。
![image](https://gyazo.com/14dc24bc22d734c03c4906a938f365b7/thumb/1000)

