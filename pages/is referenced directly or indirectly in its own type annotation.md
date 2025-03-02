---
title: "is referenced directly or indirectly in its own type annotation"
---

ts

```typescript
type m_ADD<
  REV_N extends DIGITS,
  REV_M extends DIGITS,
  CARRY extends DIGIT,
  PATH = [],
  BODY = ADD_BODY<ADD_BODY<REV_N[0], REV_M[0]>, CARRY>,
  NC = NEW_CARRY<REV_N[0], REV_M[0], CARRY>
  > = (
    {
      0: // '0' is referenced directly or indirectly in its own type annotation.
      REV_N[1] extends DIGITS ? (
        REV_M[1] extends DIGITS ? (
          m_ADD<REV_N[1], REV_M[1], NC extends DIGIT ? NC : never, [BODY, PATH]>
        ) : (
          m_ADD<REV_N[1], [0, []], NC extends DIGIT ? NC : never, [BODY, PATH]>
        )
      ) : (
        REV_M[1] extends DIGITS ? (
          m_ADD<[0, []], REV_M[1], NC, [BODY, PATH]>
        ) : (
          [NC, [BODY, PATH]]
        )
      ),
      1: never
    }[REV_N extends any ? 0 : 1]
  )
```


ts

```typescript
type m_ADD<
  REV_N extends DIGITS,
  REV_M extends DIGITS,
  CARRY extends DIGIT,
  PATH = [],
  BODY = ADD_BODY<ADD_BODY<REV_N[0], REV_M[0]>, CARRY>,
  NC = NEW_CARRY<REV_N[0], REV_M[0], CARRY>
  > = (
    {
      0:
      REV_N[1] extends DIGITS ? (
        {
          0: m_ADD<REV_N[1], REV_M[1] /* */, NC extends DIGIT ? NC : never, [BODY, PATH]>
          1: m_ADD<REV_N[1], [0, []], NC extends DIGIT ? NC : never, [BODY, PATH]>
        }[REV_M[1] extends DIGITS ? 0 : 1]
      ) : (
        {
          0: m_ADD<[0, []], REV_M[1] /* */, NC, [BODY, PATH]>
          1: [NC, [BODY, PATH]]
        }[REV_M[1] extends DIGITS ? 0 : 1]
      ),
      1: never
    }[REV_N extends any ? 0 : 1]
  )
  // Type 'REV_M[1]' does not satisfy the constraint 'DIGITS'.
```




full

ts

```typescript
type MUL<
  N extends DIGITS, M extends DIGITS,
  REV_N = REVERSE<N>,
  REV_M = REVERSE<M>,

  > = (
    REV_N extends DIGITS ? (
      REV_M extends DIGITS ? (
        m_MUL<REV_N, REV_M, []>
      ) : never
    ) : never
  )



type m_MUL<
  REV_N extends DIGITS,
  REV_M extends DIGITS,
  POWER extends DIGITS | [],
  > = (
    ADD<
      mm_MUL<REV_N, REV_M[0], POWER>,
      {
        0:

        m_MUL<REV_N, REV_M[1], [0, POWER]>,
        // Type instantiation is excessively deep and possibly infinite.

        1: [0, []]
      }[REV_M[1] extends DIGITS ? 0 : 1]
    >
  )

type mm_MUL<
  REV_N extends DIGITS,
  M extends DIGIT,
  POWER extends DIGITS | [],
  > = any;
```



