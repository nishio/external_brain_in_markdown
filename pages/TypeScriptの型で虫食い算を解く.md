---
title: "TypeScriptの型で虫食い算を解く"
---

[[TypeScriptの型]]で虫食い算を解く
1~3の相異なる値で、T1 + T2 = T3を満たすものを見つける、という簡単な問題
- 数は二進法表記して加算を1ビットの論理演算で構築
    - チャーチ数使おうとして[[TypeScriptは型を再帰的に定義できない？]]の罠にハマった
- 条件式の表現はanyかneverを返す形にした
    - 条件のand演算が型のインターセクションに対応づく
    - テストコードは結果の型に"OK"を代入する、結果がneverなら型エラーになる
- [解きたかった問題](https://twitter.com/keisei_otsuka/status/1223841916405440512?s=21)
    - 割り算は式変形で消せるので、大きめの数値型と掛け算を実装すればできるはず…
ts

```typescript
  type BIN = 0 | 1;
  type XOR<A extends BIN, B extends BIN> = (
    A extends 0 ? B : (B extends 0 ? A : 0)
  )
  type AND<A extends BIN, B extends BIN> = (
    A extends 0 ? 0 : B
  )
  type B2 = [BIN, BIN];
  type N1 = [0, 1];
  type N2 = [1, 0];
  type N3 = [1, 1];
  type ADD2DIGIT<A extends B2, B extends B2> = (
    [
      XOR<XOR<AND<A[1], B[1]>, A[0]>, B[0]>,
      XOR<A[1], B[1]>
    ]
  )
  type EQUAL<A extends B2, B extends B2> = (
    A extends B ? any : never
  );
  let a1: EQUAL<ADD2DIGIT<N1, N2>, N3> = "OK";
  // let a2: EQUAL<ADD2DIGIT<N1, N1>, N3> = "OK";  // NG

  // CONSTRAINT: T1 + T2 = T3
  type CONSTRAINT<
    T1 extends B2,
    T2 extends B2,
    T3 extends B2
    > = (
      EQUAL<ADD2DIGIT<T1, T2>, T3>
    );

  let b1: CONSTRAINT<N1, N1, N2> = "OK";
  // let b2: CONSTRAINT<N1, N1, N3> = "OK"; // NG
  let b3: CONSTRAINT<N2, N1, N3> = "OK";

  type IS_PERMUTATION<
    T1 extends B2,
    T2 extends B2,
    T3 extends B2
    > =
    T2 extends T1 ? never : (T3 extends (T1 | T2) ? never : any);

  let c1: IS_PERMUTATION<N1, N2, N3> = "OK";
  // let c2: IS_PERMUTATION<N2, N3, N2> = "OK";  // NG
  let c3: IS_PERMUTATION<N2, N1, N3> = "OK";

  type IS_SOLUTION<T1 extends B2, T2 extends B2, T3 extends B2> = (
    IS_PERMUTATION<T1, T2, T3> & CONSTRAINT<T1, T2, T3>
  );

  let d1: IS_SOLUTION<N1, N2, N3> = "OK";
  let d2: IS_SOLUTION<N2, N1, N3> = "OK";
  // let d3: IS_SOLUTION<N1, N1, N2> = "OK"; // NG
  // let d4: IS_SOLUTION<N2, N1, N2> = "OK"; // NG
```


全加算器とリンクリストを作った
- が、型エイリアスが再帰呼び出しできないためN個の型引数をとってN-1個の型引数で呼ぶとかができない
- のでADDER3がADDER2を呼ぶみたいな書き方が必要になってあまり嬉しくない
ts

```typescript
type FULL_ADDER<A extends BIN, B extends BIN, CARRY extends BIN> = (
  [
    XOR<AND<A, B>, AND<XOR<A, B>, CARRY>>,
    XOR<XOR<A, B>, CARRY>
  ]
);
type BODY<BIN2 extends [BIN, BIN]> = BIN2[1];
type CARRY<BIN2 extends [BIN, BIN]> = BIN2[0];

type LIST = BIN | [BIN, LIST]
type CAR<X extends LIST> = (
  X extends [BIN, LIST] ? X[0] : X
)
type CDR<X extends LIST> = (
  X extends [BIN, LIST] ? X[1] : never
)

type CHAIN1<
  P extends LIST, A1 extends BIN, B1 extends BIN,
  FA1 = FULL_ADDER<A1, B1, CAR<P>>
  > = (
    FA1 extends [BIN, BIN] ?
    [
      CARRY<FA1>,
      [
        BODY<FA1>,
        CDR<P>
      ]
    ] : never
  )

type ADDER2<
  A1 extends BIN, A2 extends BIN,
  B1 extends BIN, B2 extends BIN,
  P = FULL_ADDER<A2, B2, 0>
  > = (
    P extends LIST ?
    CHAIN1<P, A1, B1>
    : never
  )

type ADDER3<
  A1 extends BIN, A2 extends BIN, A3 extends BIN,
  B1 extends BIN, B2 extends BIN, B3 extends BIN,
  P = ADDER2<A2, A3, B2, B3>
  > = (
    P extends LIST ?
    CHAIN1<P, A1, B1>
    : never
  )

{
  const a1: ADDER3<1, 1, 1, 1, 1, 1> = [1, [1, [1, 0]]]
  const a2: ADDER3<1, 1, 0, 1, 1, 1> = [1, [1, [0, 1]]]
  const a3: ADDER3<1, 1, 0, 0, 1, 1> = [1, [0, [0, 1]]]
}
```

