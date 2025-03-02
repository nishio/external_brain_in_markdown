---
title: "immer"
---

![image](https://gyazo.com/f15c24829b9b7d6f349b9566daca3bdf/thumb/1000)
> Immer (German for: always) is a tiny package that allows you to work with immutable state in a more convenient way. It is based on the copy-on-write mechanism.
>  The basic idea is that you will apply all your changes to a temporary draftState, which is a proxy of the currentState. Once all your mutations are completed, Immer will produce the nextState based on the mutations to the draft state. This means that you can interact with your data by simply modifying it while keeping all the benefits of immutable data.
[https://immerjs.github.io/immer/docs/introduction](https://immerjs.github.io/immer/docs/introduction)

同じようなものを部分的に作ったり型がわけわからなくなったりしてたので素直にこれを使おう

[[updateGlobal.ts]]
updateGlobal.ts

```typescript
import { State } from "reactn/default";
import { setGlobal } from "reactn";
import { produce } from "immer";

export const updateGlobal = (update: (g: State) => void) => {
  // update global variable in destructive manner using immer
  setGlobal((g: State) => {
    return produce(g, update);
  });
};
```

usage.ts

```typescript
updateGlobal((g) => {
  g.foo.bar += g.baz.quux;
});
```





[Twitter immer mizchi](https://twitter.com/search?q=immer%20mizchi&src=typed_query&f=live)
- > immer は最高です。全人類使ってください。というか tc39 の proposal にこの仕様がほしい
- > 一時期JS/TSで絶対に副作用起こしてはいけないルールでコード書いてたんだけど、正直疲れてしまって immer を多用したり、スコープレベルで immutable を担保すればいいやみたいなところに着地した
- > immer は draft オブジェクトを書き換える時のロジックに元データを参照してしまったりしまうとごちゃごちゃするからなんか構文的にきれいに書きたいんだよな
- > immer だと
js

```javascript
const newObj = produce(obj, draft => {
  draft.x = 1;
});
```

- > のが、なんかスコープとキャプチャっぽい概念入れて
js

```javascript
const newObj = immutable do {
  obj.x = 1; // ここの変更は外に伝わらない;
  obj; // do exppression のルールで返却される
}
```

- > みたいなのがJSにほしい
- > immer の使い方わかってきたけど、これはimmerのコールバック内部で複雑な計算をしたら負けで、2ネスト以上の代入処理だけに絞るといいな
- > 流行ってない汎用ユーティリティは趣味で手を出すことはあってもよっぽどの理由じゃないと仕事じゃ採用しないことにしてて、多分唯一使ってるのが immer です。React はこれないとネストしたデータを書き換えるのつらすぎる
- > splice の引数の順番が覚えられないのは基本的にin-placeな破壊関数を避けてるからなんですが、なんで今この話をしたかというと、immer 使うと逆に純粋なオブジェクト生成のために破壊関数を書く必要があって、そこで splice を書く必要が稀に発生して思い出せなくてググるからです
