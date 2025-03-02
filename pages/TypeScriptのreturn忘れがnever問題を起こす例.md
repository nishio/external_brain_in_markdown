
[useHistory | useHooks](https://usehooks.com/useHistory/)のJSで書かれたサンプルを[[TypeScript]]に翻訳していたら、`Type 'any' is not assignable to type 'never'`になった。
原因は究極的には「網羅的でないswitch/case」で、その結果「returnされない経路がある」ことで返り値の型が T | undefined になり、それがReactのuseReducerの型推論過程で never になっている。

最初の見え方はこれ
ts

```typescript
  const [state, dispatch] = useReducer(reducer, {
    ...initialState,
    present: initialPresent
  });
```

![image](https://gyazo.com/130dbfe2c6bdd3d09caa7c73e2ad78b6/thumb/1000)

presentがneverなんだと思うじゃろ。でも全部anyにしててもダメなのじゃ。
ts

```typescript
const initialState = {
  past: [] as any[],
  present: null as any,
  future: [] as any[]
}; 
```


謎の現象が起きた時には問題を分割する。
ts

```typescript
  let x = {
    ...initialState,
    present: initialPresent
  }
  const [state, dispatch] = useReducer(reducer, x);
```

この時エラーは`useReducer(reducer, x);`のxに対して表示される。
- > Argument of type '{ present: any; past: any[]; future: any[]; }' is not assignable to parameter of type 'never'.

なので現象は「useReducerの第二引数の型がneverであると推論されている」というもの。
useReducer周りの推論の振る舞いを調べてみる
- `useReducer(null, null)`
    - > Argument of type 'null' is not assignable to parameter of type 'Reducer<any, any>'
- `useReducer(()=>1, null)`
    - > Argument of type 'null' is not assignable to parameter of type 'number'.
    - というわけで第一引数の返り値が第二引数の型だと推論されていると予想できる

ではこのケースでのreducerの型は何か？
:

```
const reducer: (state: {
    past: any[];
    present: any;
    future: any[];
}, action: any) => {
    past: any[];
    present: any;
    future: any[];
} | undefined
```

なぜかundefinedがついている(このあたりで察しがつく)

reducerの実装ではswitch/caseで4通りに分岐して、それぞれの中でreturnしている。
この4通りのケースしか存在しないことは、型システムは知らない。なのでどのケースにもマッチしないでswitch/caseを抜ける経路が存在すると考える。その結果、返り値の型にundefinedがつき、reducerの型推論の過程でそれがneverに化ける。
- (この「reducerの型推論の過程でそれがneverに化ける」の過程を深掘りしても面白いかもしれないが今回はパス)

なのでこの問題の解決法は以下の2通りある
- 手抜き: switch/caseの後ろでreturn state;して型を揃えてやる。
- 真面目: action.typeが4種類の値しかとらないことを型で宣言してやる

僕は面倒になったので手抜きの実装をした。

---
「reducerの型推論の過程でそれがneverに化ける」の過程
 ts

```
    function useReducer<R extends Reducer<any, any>>(
        reducer: R,
        initialState: ReducerState<R>,
        initializer?: undefined
    ): [ReducerState<R>, Dispatch<ReducerAction<R>>];
    
    type Reducer<S, A> = (prevState: S, action: A) => S;
    type ReducerState<R extends Reducer<any, any>> = R extends Reducer<infer S, any> ? S : never;
```

reducerの型が (T, any) => (T | undefined)である場合
- R = (T, any) => (T | undefined)
- R extends Reducer<any, any>は成功する
    - Reducer<any, any> = (any, any) => (any)だから
    - 返り値のanyに(T | undefined)が入る
- R extends Reducer<infer S, any> ? S : never はSがanyになって成功しそうな気がするのだが...
    - inferが"any"を答えることはないんだろうか
        - まあそれをありにしたら常にinferが成功するから条件式の意味がないか
        - inferの仕組み/仕様がわからないとなんともいえないな
    - infer Sが失敗してneverを返すのだろうと思う
