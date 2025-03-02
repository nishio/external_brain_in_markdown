---
title: "TypeScriptは型を再帰的に定義できない？"
---

[[TypeScriptの型]]

まとめ
- interfaceのような名前のついた型ではツリーの定義などは前からできた
- 3.7からtype aliasでも一部のケースで出来るようになった
- しかし今回やりたかったような方法での再起的定義はできない
- それをinterfaceにすることもできない
- 解決 [[TypeScriptの型で自然数を作る]]

足し算したかっただけなんだけど…
ts

```typescript
type N0 = [];
type succ<N> = [any, N];
type N1 = succ<N0>
type N2 = succ<N1>
type N3 = succ<N2>
type pred<N> = N extends [any, infer R] ? R : never;
type NEQUAL<Na, Nb> = Na extends Nb ? any : never;
type testNEQUAL = NEQUAL<pred<N2>, succ<N0>>  // any
type add<Na, Nb> = Nb extends N0 ? Na : add<succ<Na>, pred<Nb>>
// Type alias 'add' circularly references itself.
```


[https://stackoverflow.com/questions/36966444/how-to-create-a-circularly-referenced-type-in-typescript](https://stackoverflow.com/questions/36966444/how-to-create-a-circularly-referenced-type-in-typescript)
[https://github.com/microsoft/TypeScript/pull/33050](https://github.com/microsoft/TypeScript/pull/33050)
[[TypeScript]] 3.7で
ts

```typescript
type ValueOrArray<T> = T | Array<ValueOrArray<T>>;  // OK
type ValueOrArray<T> = T | ValueOrArray<Array<T>>;  // NG
```


ts

```typescript
type add<Na, Nb> = Nb extends N0 ? Na : add2<Na, Nb>;
interface add2<Na, Nb> extends add<succ<Na>, pred<Nb>> { };  // NG
// An interface can only extend an object type or intersection of object types with statically known members.
```

