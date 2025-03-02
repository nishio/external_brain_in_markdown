
[[TypeScriptの型]]

ts

```typescript
type N_ZERO = []
type NUM = N_ZERO | [NUM]
type INC<N> = [N]
type DEC<N> = (
  N extends [infer M]
  ? M
  : never
)
{
  let x: DEC<INC<N_ZERO>> = [];
}
type ADD<N, M> = (
  M extends N_ZERO
  ? N
  :
  // ADD<INC<N>, DEC<N>>
  // Type alias 'ADD' circularly references itself.
  {
    0: ADD<INC<N>, DEC<M>>,
    1: never
  }[N extends any ? 0 : 1]
)
{
  let x: ADD<[[]], [[]]> = [[[]]];  // 1 + 1 == 2
}
type N_ONE = INC<N_ZERO>;
type MUL<N, M, S = N_ZERO> = (
  M extends N_ZERO
  ? S
  :
  {
    0: MUL<N, DEC<M>, ADD<S, N>>,
    1: never
  }[N extends any ? 0 : 1]
)

type N_TWO = INC<N_ONE>
type N_THREE = INC<N_TWO>
{
  let x: MUL<N_ONE, N_ONE> = [[]];  // 1 * 1 == 1
} {
  let x: MUL<N_TWO, N_ONE> = [[[]]];  // 2 * 1 == 2
} {
  let x: MUL<N_ONE, N_TWO> = [[[]]];  // 1 * 2 == 1
} {
  let x: MUL<N_TWO, N_TWO> = [[[[[]]]]];  // 2 * 2 == 4
}
```


ts

```typescript
type N_0 = N_ZERO;
type N_1 = N_ONE;
type N_2 = N_TWO;
type N_3 = [N_2];
type N_4 = [N_3];
type N_5 = [N_4];
type N_6 = [N_5];
type N_7 = [N_6];
type N_8 = [N_7];
type N_9 = [N_8];
type N_TEN = [N_9];

type DIGITS2<N, M> = MUL<N, N_TEN, M>

// try "N - M", return answer or null
type MINUS<N, M> = (
  M extends N_0
  ? N
  : (
    {
      0: null,
      1: MINUS<DEC<N>, DEC<M>>
    }[N extends N_0 ? 0 : 1]
  )
)

{
  let x: MINUS<N_5, N_2> = {} as N_3
} {
  let x: MINUS<N_2, N_5> = null;
}

type DIVIDE<
  N, M,
  Q = N_0,
  N1 = MINUS<N, M>
  > = (
    {
      0: [Q, N],
      1: DIVIDE<N1, M, INC<Q>>
    }[N1 extends null ? 0 : 1]
  )
{
  let x: DIVIDE<MUL<N_3, N_4>, N_TEN> = {} as [N_1, N_2]
}
{
  let x: DIVIDE<MUL<N_7, N_8>, N_TEN> = {} as [N_5, N_6]
  // Type instantiation is excessively deep and possibly infinite.
}
```

5 * 6 == 30 はできるけど 6 * 7 == 42 はできない
