
99+7=107の繰り上がり演算ができている
掛け算もやろうとしたが[[掛け算がうまくいかない]]
- [[変なexcessively deepの最小限の例]]
ts

```typescript
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
let s = "";
digits.forEach((x) => { s += `${x} | ` })
console.log(s)
type DIGIT = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9;

let obj = {}
digits.forEach((x) => {
  let row = {}
  digits.forEach((y) => {
    row[y] = (x + y) % 10
  })
  obj[x] = row
})
console.log(obj)
type ADD_BODY<N extends DIGIT, M extends DIGIT> = (
  {
    0: { 0: 0, 1: 1, 2: 2, 3: 3, 4: 4, 5: 5, 6: 6, 7: 7, 8: 8, 9: 9 }
    1: { 0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, 6: 7, 7: 8, 8: 9, 9: 0 }
    2: { 0: 2, 1: 3, 2: 4, 3: 5, 4: 6, 5: 7, 6: 8, 7: 9, 8: 0, 9: 1 }
    3: { 0: 3, 1: 4, 2: 5, 3: 6, 4: 7, 5: 8, 6: 9, 7: 0, 8: 1, 9: 2 }
    4: { 0: 4, 1: 5, 2: 6, 3: 7, 4: 8, 5: 9, 6: 0, 7: 1, 8: 2, 9: 3 }
    5: { 0: 5, 1: 6, 2: 7, 3: 8, 4: 9, 5: 0, 6: 1, 7: 2, 8: 3, 9: 4 }
    6: { 0: 6, 1: 7, 2: 8, 3: 9, 4: 0, 5: 1, 6: 2, 7: 3, 8: 4, 9: 5 }
    7: { 0: 7, 1: 8, 2: 9, 3: 0, 4: 1, 5: 2, 6: 3, 7: 4, 8: 5, 9: 6 }
    8: { 0: 8, 1: 9, 2: 0, 3: 1, 4: 2, 5: 3, 6: 4, 7: 5, 8: 6, 9: 7 }
    9: { 0: 9, 1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 7, 9: 8 }
  }[N][M]
)

{
  const x1: ADD_BODY<1, 2> = 3;
  const x2: ADD_BODY<9, 8> = 7;
}

obj = {}
digits.forEach((x) => {
  let row = {}
  digits.forEach((y) => {
    row[y] = Math.trunc((x + y) / 10)
  })
  obj[x] = row
})
console.log(obj)

type ADD_CARRY<N extends DIGIT, M extends DIGIT> = (
  {
    0: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 0 }
    1: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 1 }
    2: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 1, 9: 1 }
    3: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 1, 8: 1, 9: 1 }
    4: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 1, 7: 1, 8: 1, 9: 1 }
    5: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
    6: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
    7: { 0: 0, 1: 0, 2: 0, 3: 1, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
    8: { 0: 0, 1: 0, 2: 1, 3: 1, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
    9: { 0: 0, 1: 1, 2: 1, 3: 1, 4: 1, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
  }[N][M]
)

obj = {}
digits.forEach((x) => {
  let row = {}
  digits.forEach((y) => {
    row[y] = (x * y) % 10
  })
  obj[x] = row
})
console.log(obj)

type MUL_BODY<N extends DIGIT, M extends DIGIT> = (
  {
    0: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 0 }
    1: { 0: 0, 1: 1, 2: 2, 3: 3, 4: 4, 5: 5, 6: 6, 7: 7, 8: 8, 9: 9 }
    2: { 0: 0, 1: 2, 2: 4, 3: 6, 4: 8, 5: 0, 6: 2, 7: 4, 8: 6, 9: 8 }
    3: { 0: 0, 1: 3, 2: 6, 3: 9, 4: 2, 5: 5, 6: 8, 7: 1, 8: 4, 9: 7 }
    4: { 0: 0, 1: 4, 2: 8, 3: 2, 4: 6, 5: 0, 6: 4, 7: 8, 8: 2, 9: 6 }
    5: { 0: 0, 1: 5, 2: 0, 3: 5, 4: 0, 5: 5, 6: 0, 7: 5, 8: 0, 9: 5 }
    6: { 0: 0, 1: 6, 2: 2, 3: 8, 4: 4, 5: 0, 6: 6, 7: 2, 8: 8, 9: 4 }
    7: { 0: 0, 1: 7, 2: 4, 3: 1, 4: 8, 5: 5, 6: 2, 7: 9, 8: 6, 9: 3 }
    8: { 0: 0, 1: 8, 2: 6, 3: 4, 4: 2, 5: 0, 6: 8, 7: 6, 8: 4, 9: 2 }
    9: { 0: 0, 1: 9, 2: 8, 3: 7, 4: 6, 5: 5, 6: 4, 7: 3, 8: 2, 9: 1 }
  }[N][M]
)

obj = {}
digits.forEach((x) => {
  let row = {}
  digits.forEach((y) => {
    row[y] = Math.trunc((x * y) / 10)
  })
  obj[x] = row
})
console.log(obj)

type MUL_CARRY<N extends DIGIT, M extends DIGIT> = (
  {
    0: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 0 }
    1: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0, 7: 0, 8: 0, 9: 0 }
    2: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 0, 5: 1, 6: 1, 7: 1, 8: 1, 9: 1 }
    3: { 0: 0, 1: 0, 2: 0, 3: 0, 4: 1, 5: 1, 6: 1, 7: 2, 8: 2, 9: 2 }
    4: { 0: 0, 1: 0, 2: 0, 3: 1, 4: 1, 5: 2, 6: 2, 7: 2, 8: 3, 9: 3 }
    5: { 0: 0, 1: 0, 2: 1, 3: 1, 4: 2, 5: 2, 6: 3, 7: 3, 8: 4, 9: 4 }
    6: { 0: 0, 1: 0, 2: 1, 3: 1, 4: 2, 5: 3, 6: 3, 7: 4, 8: 4, 9: 5 }
    7: { 0: 0, 1: 0, 2: 1, 3: 2, 4: 2, 5: 3, 6: 4, 7: 4, 8: 5, 9: 6 }
    8: { 0: 0, 1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 4, 7: 5, 8: 6, 9: 7 }
    9: { 0: 0, 1: 0, 2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 7, 9: 8 }
  }[N][M]
)

type DIGITS = [DIGIT, []] | [DIGIT, DIGITS]

type REVERSE<N extends DIGITS, S = []> = (
  N[1] extends DIGITS
  ?
  // REVERSE<N[1], [N[0], S]>
  { 0: REVERSE<N[1], [N[0], S]> }[N extends any ? 0 : 0]
  : [N[0], S]
)

{
  let x: REVERSE<[1, [2, [3, []]]]> = [3, [2, [1, []]]]
}

type ADD<
  N extends DIGITS, M extends DIGITS,
  REV_N = REVERSE<N>,
  REV_M = REVERSE<M>,

  > = (
    REV_N extends DIGITS ? (
      REV_M extends DIGITS ? (
        m_ADD<REV_N, REV_M, 0>
      ) : never
    ) : never
  )

type NEW_CARRY<N extends DIGIT, M extends DIGIT, CARRY extends DIGIT> = (
  ADD_BODY<
    ADD_CARRY<N, M>,
    ADD_CARRY<ADD_BODY<N, M>, CARRY>
  >
)

{
  let x1: NEW_CARRY<0, 0, 0> = 0;
  let x2: NEW_CARRY<5, 5, 0> = 1;
  let x3: NEW_CARRY<5, 4, 0> = 0;
  let x4: NEW_CARRY<5, 4, 3> = 1;
}

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
          0: m_ADD<
            REV_N[1],
            REV_M[1] extends DIGITS ? REV_M[1] : never,
            NC extends DIGIT ? NC : never,
            [BODY, PATH]
          >
          1: m_ADD<
            REV_N[1],
            [0, []],
            NC extends DIGIT ? NC : never,
            [BODY, PATH]
          >
        }[REV_M[1] extends DIGITS ? 0 : 1]
      ) : (
        {
          0: m_ADD<
            [0, []],
            REV_M[1] extends DIGITS ? REV_M[1] : never,
            NC extends DIGIT ? NC : never,
            [BODY, PATH]
          >
          1: [NC, [BODY, PATH]]
        }[REV_M[1] extends DIGITS ? 0 : 1]
      ),
      1: never
    }[REV_N extends any ? 0 : 1]
  )

{
  let x1: ADD<[1, []], [2, []]> = [0, [3, []]];
  let x2: ADD<[9, []], [8, []]> = [1, [7, []]];
  let x3: ADD<[9, [9, []]], [8, []]> = [1, [0, [7, []]]];
}
```
