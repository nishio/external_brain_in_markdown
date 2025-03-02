---
title: "TypeScript types memo"
---

[[TypeScriptの型]]

- `T1 extends T2 ? F<T1> : never`
    - similar to `f(t1 as T2)`
- circularly references
    - `{0: T1}[T extends any ? 0 : 0]`
    - `{0: T1, 1: T2}[CONDITION ? 0 : 1]`
        - `CONDITION ? T1 : T2`

ts

```typescript
// type GET_LAST<X extends LIST> = 
//   X extends [BIN, LIST] ? CAR<X> : GET_LAST<CDR<X>>
// NG: Type alias 'GET_LAST' circularly references itself.

type GET_LAST<X extends LIST> = { 
  0: CAR<X>, 
  1: GET_LAST<CDR<X>> 
}[X extends [BIN, LIST] ? 0 : 1]
// OK
```

- CONDITION
    - `N extends any`
        - true
        - `any extends any` does not work
    - true: any, false: never
        - `N extends M ? ... : ...`の形でしか使えない
