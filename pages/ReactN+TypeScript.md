
[[ReactN]]を[[TypeScript]]で使うときにArgument of type '"a"' is not assignable to parameter of type 'never'.が出たのを、マニュアル読まずにフィーリングで直したら、実は直ってなかったので、正しい直し方をメモ。
[[TypeScriptの型]]
ts

```typescript
import { useGlobal, setGlobal } from 'reactn';
const INITIAL_STATE = {
  a: 1,
  b: "foo",
}
type TState = typeof INITIAL_STATE;
//type TState = {a: number; b: string;}
setGlobal(INITIAL_STATE);

const App: React.FC = () => {
  const a = useGlobal("a");
  // ERROR: Argument of type '"a"' is not assignable to parameter of type 'never'.
...
```


useGlobalに型指定を付けたらコンパイルエラーがなくなったのでそれで良いのかと思ったら、型がおかしくなっていて後から問題が起きた。
ts

```typescript
  const [a] = useGlobal<TState>("a");
  // no compile error, it seems OK but...
  // const a: string | number
  // So,
  console.log(a + 1);
  // Operator '+' cannot be applied to types 'ReactText' and 'number'.
```


正しい直し方 [https://github.com/CharlesStover/reactn/blob/master/README.md#typescript-support](https://github.com/CharlesStover/reactn/blob/master/README.md#typescript-support)
ts

```typescript
declare module 'reactn/default' {
  export interface State extends TState { }
}

const App: React.FC = () => {
  const [a] = useGlobal("a");  // OK, no generics needed
  console.log(a + 1);  // OK
```


the reason why `a: string | number`
ts

```typescript
useGlobal<TState>("a");
// return value: StateTuple<{
//   a: number;
//   b: string;
// }, "a" | "b">
```


ts

```typescript
useGlobal<G extends {} = State, Property extends keyof G = keyof G>(property: Property): StateTuple<G, Property>;

export type StateTuple<G extends {}, P extends keyof G> = [
  G[P],
  Setter<G, P>,
];
```


この原因は型引数を2つとるgenericsに1つ指定するともう1つの型がかわることが原因。
型引数を指定しない場合は引数から型Keyが推論され、それは文字列のリテラルタイプになる。
一方Dictに型を渡した場合、 KeyはDictのkeyofになる。この場合、すべてのキーのユニオン型になる。
ts

```typescript
interface DefaultDict {
  a: number,
  b: string,
}
const dict: DefaultDict = {
  a: 1,
  b: "foo"
}
const bar: <
  Dict extends {} = DefaultDict,
  Key extends keyof Dict = keyof Dict
  >(key: Key) => Key
  = (key) => key;

const a1 = bar("a");
// const a1: "a"

const a2 = bar<typeof dict>("a");
// const a2: "a" | "b"

const a3 = bar<DefaultDict>("a");
// const a3: "a" | "b"
```


`StateTuple[0]`の`G[P]`でPがすべてのキーのユニオン型なので、`G[P]`はすべてのバリューのユニオン型になる
ts 

```
 export type StateTuple<G extends {}, P extends keyof G> = [
   G[P],
   Setter<G, P>,
 ];
```

