---
title: "2日掛けてanyを撲滅した"
---

元タイトル「anyをunknownに変える」
変えた結果、8〜9割のanyはunknownの状態に留まらなかったのでタイトルを変えた。

---

[[TypeScript]]で手抜きしてanyを使っている箇所って「自分の書いたコードだけど型をきちんと書くのが面倒だからanyにしてる」って場合と「サードパーティのライブラリからやってくる値で、型がなんなのか調べるのが面倒だからanyにしている」ってケースがある。

例えば後者の例で、Firestoreから取ってきたドキュメントオブジェクトの型がよくわからないのでanyにしていた。
ts

```typescript
(doc: any) => { ... }
```


これをunknownに変えると…
ts

```typescript
(doc: unknown) => { ... }
```


unknownにexistsが生えてるかどうか知らないぞ、と指摘される。
きちんとした型をつける必要があるのだが、どうすれば良いか？
ts

```typescript
if (doc.exists) {  // ERROR: Object is of type 'unknown'.  TS2571
```


それに必要な情報を得るために、あり得ない型を付けてみる。
ts

```typescript
(doc: number) => { ... }
```


そうすると型の互換性エラーでどういう型が期待されているのか表示される。
> Argument of type '(doc: number) => void' is not assignable to parameter of type '(value: DocumentSnapshot<DocumentData>) => void | PromiseLike<void>'.

`DocumentSnapshot<DocumentData>`だという名前がわかったのでそれで検索してみるとリファレンスが見つかる
- [DocumentSnapshot | JavaScript SDK  |  Firebase](https://firebase.google.com/docs/reference/js/firebase.firestore.DocumentSnapshot)

長いので別名をつけることにした
ts

```typescript
type Document = firebase.firestore.DocumentSnapshot<firebase.firestore.DocumentData>;
...
(doc: Document) => { ... }
```


この後、別のエラーが出る
ts

```typescript
JSON.parse(data.json)  // ERROR: Object is possibly 'undefined'.  TS2532
```

Firestoreの解説通りに`doc.exists`で存在を確認してから`data = doc.data()`で取得しているので、undefinedになることはないはずだが、TypeScriptはそんなこと知らない。

そこで例外を投げることにする。
ts

```typescript
if (data === undefined) {
  throw new TypeError("doc.data is undefined");
}
```

こうすることで、ここ以降のフローではundefinedの可能性が消える。TypeScriptはそれをちゃんと理解する。

ところで昔は「無視したら処理を続行できそうなら例外を投げるのはやめとこ」って思ってたのだけど、[[Sentry]]を使うようになって「ならないはずの状態になってるのを検知したら速やかに例外を投げとけば通知が来るからバグを見つけやすい」と考え方が変わった。ユーザのブラウザ上での例外が開発者に届くことはプログラミングに対する考え方にも影響するのだな。

---
anyを全部一度にunknownに変えて大変だった。一つずつやるべきだった。複雑な問題が起きた時に切り分けが難しくなる。
- [[React.forwardRef]]にハマった
    - FCをラップするための関数なのに「FCだ」と型宣言するとダメ、宣言しなければOK
    - forwardRefをFCを受け取れるように実装するべきなのでは。

結局unknownのままでは使えないのできちんと型を書く羽目になり、unknownも大体消える。
anyからunknownに変えることで型チェックが走るようにして、エラー内容を見ながら適切な型に変える、という移行プロセスなんだなぁと思った

unknownは1箇所だけしか残らなかった
- `onClick: () => unknown`
- 返り値がvoidなのかそうでないのか確認してないけど、使わないのでどっちでもいいや、ということで残ることになった。

---
何年も前に書き始めたプロジェクトのソースコードをanyで検索して処理してみる
TypeScriptを学びながら書いたので結構anyがある。

- 1日目: 4ポモドーロで124個あったanyが56個になった
    - anyが良くある場所
        - Firebaseとのやりとり
            - doc.data()がどんなメンバーを持ってるかとかTypeScriptは知りようがない
        - MouseEventとかTouchEventとかをanyで受けてた
            - 「ここはTouchEventだな！」と書き換えたら「TouchEventならこのメンバー持ってないと思いますけど…」って突っ込まれる、ぐぬぬ
                - この件、ReactのTouchの定義がradiusXを持ってないことがわかった
                    - これは標準ではないがiPadのSafariで使えるので使いたい
            - Paper.jsがラップしてToolEventにして渡してくるところもある
                - ToolEvent.eventに実際は生のイベントを持ってるのに、型の上では持ってないことになってる不整合がある
    - 型を故意に衝突させたり、マウスホバーして処理系がつけた型を読んだりするテクニックを身につける前に書いたコードが、複雑な型がわからなくてanyにしてるケースが多い
        - そういうのはすぐ直せるから楽
    - サードパーティのコードが自分の期待に合わない場合、ズレをどこかで吸収する必要があるわけだが、型をanyにする方法ではその値とそこから派生する値のつかられる箇所すべてで型チェックが無効になるのに対し、ts-ignoreならその1箇所のみで無効になるので影響範囲を限定できる。
    - 型がついてないことによる根本的に悪い設計と思しきものにぶつかって、設計から変えないと小手先の変更ではダメな感じがしてきた

- 2日目: ほぼ全部消えた
    - `return (x as any).item !== undefined;`は`return "item" in x;`でいい
    - React Routerでcomponentの型は何か
        - `<Route path="/:id" component={MyComponent} />`
        - `<Route path="/:id" component={1} />`ってやっても`Type 'number' is not assignable to type 'FunctionComponent<any> | ComponentClass<any, any> | ComponentClass<RouteComponentProps<any, StaticContext, PoorMansUnknown>, any> | FunctionComponent<...> | undefined'`とか言うので参考にならない
        - 正解は`const MyComponent: React.FC<RouteComponentProps<{ id: string }>>`
    - Firestoreはundefinedを含む値を保存しようとするとエラーになるようだ
        - `{x: 1}` はOKで `{x: 1, y: undefined}`はNGということになる
        - TypeScriptの型ではこの2つは区別できない
        - `{ x: number; y: number | null }`みたいな型で、yがない時は`{ x: 1, y: null };`とやる
    - `obj.foo = convertType(obj.foo)`みたいに型の違うものでメンバを上書きをするような書き方はやめる必要がある
        - そもそも「型を変えてメンバを入れ直したオブジェクト」は「別物」なのだから型が異なっているわけで、それを一つの変数でやろうとするから型をつけられなくなる
        - `new_obj = {...obj, foo: convertType(obj.foo)}`
    - オブジェクトに順番に値を入れていって完成させるような書き方もやめる必要がある
        - Bad
ts

```typescript
export const createFoo = (): FOO => {
  const ret: any = {
    version: 2,
  };
  ret.items = [];
  return ret;
};
```

        - Good
ts

```typescript
export const createFoo = (): FOO => {
  const version = 2;
  const items: ItemID[] = [];
  return { version, items };
};
```

            - 前者のようにanyにしてると、この関数が作ったオブジェクトが本当にFOO型であるかはチェックされない
    - `e: paper.ToolEvent`は本当は`e.event`を持っているが、型の上では無いことになっている
        - 以前は`const event = (e as any).event;`と書いていた
ts

```typescript
// const event = e.event; // Property 'event' does not exist on type 'ToolEvent'
const event = (e as any).event; // event: any
```

        - anyを消すならこうかな？
ts

```typescript
// @ts-ignore
const event: MouseEvent = e.event;
```

    - こういうのの組み合わせで、ブラウザ上の状態をFirestoreに保存できるオブジェクトに変換する関数を下記のように書き変えた
        - positionがpaper.Pointオブジェクトなのがダメなので`[number, number]`にしたり
        - 保存する値だけを取り出したり
        - before
ts

```typescript
export const convertStateItemToFirestore = (x: StateItem) => {
  const ret: any;
  ret.type = x.type;
  ret.id = x.id;
  ret.position = [x.position.x, x.position.y]
  if (isPieceStateItem(x)) {
    ret.text = x.text;
	...	
  } else if (isPathStateItem(x)) {
    ret.opacity = x.opacity ?? 1.0;
	...
  }
  return ret;
}
```

        - after
ts

```typescript
export const convertStateItemToFirestore = (x: StateItem) => {
  const { type, id } = x;
  const position: [number, number] = [x.position.x, x.position.y];
  const common = { type, id, position };
  if (isPieceStateItem(x)) {
    const { text, compact, scale } = x;
    return {...common, text, compact, scale};
  } else if (isPathStateItem(x)) {
    const { opacity, dashArray, created } = x;
    return {
      ...common, created,
      opacity: opacity ?? 1.0,
      dashArray: dashArray ?? [],
    };
  } else if (...) {
  	...
  } else {
    throw new TypeError(`unknown type: ${type}`);
  }
}
```

    - 関数を受け取って処理で包んで返す関数、これは厄介
ts

```typescript
export const onOverlayCanvas = (f: (...args: any[]) => unknown) => {
  return (...args: unknown[]) => {
    paper.projects[1].activate();
    const ret = f(...args);
    paper.projects[0].activate();
    return ret;
  };
};
```

        - なんとかするためにはジェネリクスが必要になった
ts

```typescript
import { ToolEvent } from "paper";

export const onOverlayCanvas = <T extends [ToolEvent] | []>(
  f: (...args: T) => unknown,
) => {
  return (...args: T) => {
    paper.projects[1].activate();
    const ret = f(...args);
    paper.projects[0].activate();
    return ret;
  };
};
```

- Firestoreから過去のデータを読むことができないというバグを入れてしまった
    - `isReadOnly: bool`だと思い込んでたがtrueの時しかエントリーがなかった
    - [[無意識に例外を握りつぶしてた]]ことが原因で、バグの原因の特定に時間が掛かった
- 124個あったanyが3個になった
    - うち2つはコメントやメッセージ文字列の中身
    - 最後の1つはデバッグの便利さのために作ってあるデバッグオブジェクトの型
    - unknownは16個
        - 8〜9割のanyはunknownに変わるのではなくまともな型に変わった

追記 2021-02-18 [[any消し祭りのゴミ片付け]]
- [[requireしたものはanyになる]]
    - これが原因でPaper.jsを使うコードに無自覚のanyがあった
    - 修正してpaper.Itemが型チェックされるようになった
- [[クラスのインスタンスをspreadしてもメソッドは複製されない]]
    - なのでキャストで解決した。あちこちにキャストがあるのも良くないので一箇所にまとめた
ts

```typescript
export const attachStateItem = (
  paperItem: paper.Item,
  stateItem: StateItem,
): PaperItem => {
  const ret = paperItem as PaperItem;
  ret.item = stateItem;
  return ret;
};
```


