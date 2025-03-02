---
title: "circularly references itself"
---

Type alias 'REVERSE' circularly references itself

ts

```typescript
{
  // type REVERSE<N extends DIGITS, S = []> = (
  //   REVERSE<N[1], [N[0], S]>
  // )
  // NG: Type alias 'REVERSE' circularly references itself.
}
{
  type REVERSE<N extends DIGITS, S = []> = (
    N[1] extends DIGITS
    ? { 0: REVERSE<N[1], [N[0], S]> }[N extends any ? 0 : 0]
    : [N[0], S]
  )
}
{
  // type REVERSE<N extends DIGITS, S = []> = (
  //   {
  //     0: REVERSE<N[1] /* */, [N[0], S]>,
  //     1: [N[0], S]
  //   }[N[1] extends DIGITS ? 0 : 1]
  // )
  // NG: Type 'N[1]' does not satisfy the constraint 'DIGITS'.
}
{
  type REVERSE<N extends DIGITS, S = []> = (
    {
      0: REVERSE<N[1] extends DIGITS ? N[1] : never, [N[0], S]>,
      1: [N[0], S]
    }[N[1] extends DIGITS ? 0 : 1]
  )
}
```


