
型の検証は実行を伴わないので、実行するコードがない疑似コードであっても型の整合性があるかどうか検証できる

「とりあえずStateってものがあるんだ」を表現する
ts

```typescript
type State = "State"
```

Stateを"State"というリテラルタイプにしている
なぜか
TypeScriptは[[構造的型付け]]なので適当に空オブジェクトなどにしてしまうと、適切でない代入をしてもエラーにならないため
ts

```typescript
type State = {};
type Other = {};

 (x: State) => {
   const y: Other = x;  // エラーにならない
 }
```


「MutexはState型の値を持っている」を表現する
ts

```typescript
type Mutex = {
  state: State,
};
```


「Stateまたはnull」を表現する
ts

```typescript
type Mutex = {
  state: State | null,
};
```


「Stateを取ってStateを返す関数updateStateがある」
ts

```typescript
let updateState: (state: State) => State;
```

ここでは関数の型の宣言だけをして、関数の実装を定義はしていない。
letは宣言のタイミングで値を持たなくてもOKなのを利用している。

ts

```typescript
let foo: (arg: ArgType) => RetType
```

実装をするとこう書き換わる
ts

```typescript
const foo = (arg: ArgType): RetType => { ... }
```


ts

```typescript
type Foo = "Foo";
const createFoo = (): Foo => {
  // ...
  return "Foo";
}
```



「T型のリストで、最低2個ある」
ts

```typescript
[T, T, ...T[]]
```


