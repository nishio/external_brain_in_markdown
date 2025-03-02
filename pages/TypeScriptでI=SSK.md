
[[TypeScriptの型]]
ts

```typescript
let I: <T>(x: T) => T;
let K: <T1, T2>(x: T1) => ((y: T2) => T1) = (x) => {
  return (y) => x;
};
let S: <Tz, Tyz, Ts>(x: (z: Tz) => ((yz: Tyz) => Ts)) => ((y: (z: Tz) => Tyz) => ((z: Tz) => Ts)
) = (x) => {
  return (y) => {
    return (z) => {
      return x(z)(y(z));
    }
  }
}
let SKK = S(K)(K);
I = SKK;
let x: 0 = SKK(0);
```


VSCodeの自動インデントで比較的まともな見栄えにならないかなと少し工夫してみた
ts

```typescript
let S: <Tz, Tyz, Ts>
  (x: ((z: Tz) => ((yz: Tyz) => Ts)))
  =>
  (y: (z: Tz) => Tyz)
    =>
    (z: Tz)
      => Ts
  =
  (x) => (
    (y) => (
      (z) => (
        x(z)(y(z))
      )
    )
  )
```


ts

```typescript
{
  type Tx<Txx> = (x: Tx<Txx>) => Txx
  let M: <Txx>(x: Tx<Txx>) => Txx = (x) => (x(x));
}
```


次はこれからanyを消すパズルです
ts

```typescript
let iota: (x: any) => any = (x) => x(S)(K);
let I = iota(iota);
```


うーん、素朴にやったら謎の型ができてしまった
ts

```typescript
  type Ts = typeof S;
  type Tk = typeof K;
  let xs: <Tr>(x: (s: Ts) => Tr) => Tr = (x) => x(S);
  let yk: <Tr>(y: (k: Tk) => Tr) => Tr = (y) => y(K);

  let iota: <Txsk>(x: (s: Ts) => (k: Tk) => Txsk) => Txsk = (x) => x(S)(K);
  //let I = iota(iota);  // エラーメッセージは下記

  let a = S(S);
  let b = S(S)(K);  // let b: (z: (z: {}) => (yz: {}) => {}) => (z: {}) => {}
  let c = S(S)(K)(K)
```



- Argument of type
    - '<Txsk>(x: (s: <Tz, Tyz, Ts>(x: (z: Tz) => (yz: Tyz) => Ts) => (y: (z: Tz) => Tyz) => (z: Tz) => Ts) => (k: <T1, T2>(x: T1) => (y: T2) => T1) => Txsk) => Txsk'
- is not assignable to parameter of type
    - '(s: <Tz, Tyz, Ts>(x: (z: Tz) => (yz: Tyz) => Ts) => (y: (z: Tz) => Tyz) => (z: Tz) => Ts) => (k: <T1, T2>(x: T1) => (y: T2) => T1) => {}'.

    - Types of parameters 'x' and 's' are incompatible.
        - Type
            - '(y: (z: (z: {}) => (yz: {}) => {}) => (z: {}) => {}) => (z: (z: {}) => (yz: {}) => {}) => (z: {}) => {}'
        - is not assignable to type
            - '(k: <T1, T2>(x: T1) => (y: T2) => T1) => (z: {}) => {}'.

[[TypeScript]]
