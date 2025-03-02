---
title: "TypeScriptの型の練習"
---

[[TypeScriptの型]]
typescript

```typescript
const obj = {
  s: "foo",
  f: () => "bar"
}

const get1 = (key: keyof typeof obj) => {
  return obj[key]
}
// const get1: (key: "s" | "f") => string | (() => string)

const get2 = (key: keyof typeof obj) => {
  const value = obj[key]
  if (typeof value === "string") {
    return value
  } else {
    return () => value()
  }
}
// const get2: (key: "s" | "f") => string | (() => string)
```


元ネタ [https://twitter.com/teramotodaiki/status/1214149145935532033](https://twitter.com/teramotodaiki/status/1214149145935532033)

ts

```typescript
function get4<Key extends keyof typeof obj>(key: Key): typeof obj[Key] {
  return obj[key];
}

// ERROR
// function get5<Key extends keyof typeof obj>(key: Key): typeof obj[Key] extends string ? string : () => string {
//   return obj[key];
// }

function get6<Key extends keyof typeof obj>(key: Key): any {
  const value = obj[key]
  if (typeof value === "string") {
    return value
  } else {
    return () => value() // ERROR
    // This expression is not callable.
    // Not all constituents of type 'string | (() => string)' are callable.
    //   Type 'string' has no call signatures.
  }
}
```


`key`
- get2
    - `keyof typeof obj` === `"s" | "f"`なので
    - `(parameter) key: "s" | "f"`
- get4
    - `(parameter) key: Key extends "s" | "f"`

`const value = obj[key]`
- get2
    - `const value: string | (() => string)`
- get6
ts

```typescript
const value: {
    s: string;
    f: () => string;
}[Key]
```


要するに元ネタのコードでは余計なextendsのせいでkeyの型が`"s" | "f"`だとわからなくなっており、
その結果`obj[key]`も`string | (() => string)`だとわからなくなっている
`string | (() => string)`ならUnion Typeなので[Type Guards](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types)が使えるがget6の方は複雑な型なのでそれができない
(可能だが現時点のTSがサポートしてない)
なのでelse節のvalueが`() => string`であることがわからず`Type 'string' has no call signatures`になる

---

`const x = get2("f")  // const x: string | (() => string)`
うーん、そりゃそうか、関数が呼ばれる前にobjが書き換わる可能性があるからな

ts

```typescript
const x2 = get7("s")  // const x2: string
const x3 = get7("f")  // const x3: () => string
```

こういう挙動が欲しい場合、

ts

```typescript
function get7(key: "s"): string;
function get7(key: "f"): (() => string);
function get7(key: "s" | "f"): (string | (() => string)) {
  const value = obj[key]
  if (typeof value === "string") {
    return value
  } else if (typeof value === "function") {
    return () => value()
  }
}
```

となるか

[[TypeScript]]の[[型]]の練習
