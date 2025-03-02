---
title: "Runtypes と io-ts のoptionalの比較"
---

まず普通のTypeScriptの型がコード上とVSCodeのヒント上でどう見えるか
- なるべくこれに近い書き方・見え方だと楽
ts

```typescript
// typescript
{
  type OptionalY = { x: number; y?: number };
  const value1: OptionalY = { x: 1 };
  const value2: OptionalY = { x: 1, y: 2 };
}
```

![image](https://gyazo.com/0dbfd6c60848295b0e3e48c569716ac8/thumb/1000)

Runtypesの場合
- 型オブジェクトは「まあ逐語訳で読めるかな」という感じ
- 生成された静的型はまったくTypeScriptのものと同じ
ts

```typescript
// runtypes
{
  const RT_OpeionalY = Record({ x: Number, y: Optional(Number) });
  type OptionalY = Static<typeof RT_OpeionalY>;
  const value1: OptionalY = { x: 1 };
  const value2: OptionalY = { x: 1, y: 2 };
}
```

![image](https://gyazo.com/6d3f4f112bef34630d8d35e7213abce4/thumb/1000)
![image](https://gyazo.com/8887af7557d6b24987f8aac41fe6cd02/thumb/1000)

io-tsの場合
- まずは公式ドキュメントで解説されてたpartialとのintersectionを作る書き方
- 静的型の方は、まあ真ん中の`} & {`の解釈で戸惑わないレベルのプログラマならさほど実害はないか？
- 型オブジェクトの方は…ここから「yはオプションである」と読み取るのは認知コスト高そう
ts

```typescript
// io-ts, official solution
{
  const IO_OpeionalY = t.intersection([
    t.type({
      x: t.number,
    }),
    t.partial({
      y: t.number,
    }),
  ]);
  type OptionalY = t.TypeOf<typeof IO_OpeionalY>;
  const value1: OptionalY = { x: 1 };
  const value2: OptionalY = { x: 1, y: 2 };
  // const value3: OptionalY = { x: 1, y: "foo" };
  // expected ERROR: Type 'string' is not assignable to type 'number | undefined'.
}
```

![image](https://gyazo.com/96aaa9ff55003b6b06b14b08331665d4/thumb/1000)
![image](https://gyazo.com/ba29ab9ae416674b103b7f6f03f8f99c/thumb/1000)

io-tsの一見上手くいきそうなユーティリティ関数を作るアプローチ(実はまったく上手くいかない)
- value3の例ではoptionalなnumberにstringを入れる間違いを検出できてなくて全然ダメ
    - 僕はtsconfigの[No Implicit Any](https://www.typescriptlang.org/tsconfig#noImplicitAny)をRecommendedのtrueにしているのでそもそもこのコードはエラーになる。
    - デフォルトのfalseの場合も指摘はされる: `Parameter 'tp' implicitly has an 'any' type, but a better type may be inferred from usage.`
        - つまりtpがany
        - なのでそれが伝播してyもanyになっている、これがvalue3の問題の原因
- またvalue1のように「yが存在しない」というパターンは型エラーになるべきではないが、なってしまう
ts

```typescript
// io-ts
{
  const optional = (tp) => t.union([tp, t.undefined]);
  const IO_OpeionalY = t.type({
    x: t.number,
    y: optional(t.number),
  });
  type OptionalY = t.TypeOf<typeof IO_OpeionalY>;
  // const value1: OptionalY = { x: 1 };
  // ERROR: Property 'y' is missing in type '{ x: number; }' but required in type '{ x: number; y: any; }'
  const value2: OptionalY = { x: 1, y: 2 };
  const value3: OptionalY = { x: 1, y: "foo" }; // unexpected OK
}
```

![image](https://gyazo.com/7f01f7afef7ae573ee855b64d4e355d4/thumb/1000)
- value3のanyの問題を解決するにはジェネリクスを使う方法がある
    - ただしこの方法でもvalue1のメンバー不在の問題は解決されない
ts

```typescript
{
  const optional = <T extends t.Mixed>(tp: T) => t.union([tp, t.undefined]);
  const IO_OpeionalY = t.type({
    x: t.number,
    y: optional<typeof t.number>(t.number),
  });
  type OptionalY = t.TypeOf<typeof IO_OpeionalY>;
  // const value1: OptionalY = { x: 1 };
  // ERROR: Property 'y' is missing in type '{ x: number; }' but required in type '{ x: number; y: any; }'
  const value2: OptionalY = { x: 1, y: 2 };
  // const value3: OptionalY = { x: 1, y: "foo" };
  // expected ERROR: Type 'string' is not assignable to type 'number | undefined'
}
```


追記
- 上記の通りメンバーが不在なオブジェクトを生成された静的型の変数に代入することは型エラーになるが、decode結果から代入する時にはエラーなく入る
- decode結果はJestのtoEqualの比較でもJSON.stringify結果での比較でも元のオブジェクトと同一に見えるが、実はentriesでは異なる
    - 要するにdecodeの段階でyが存在しないのではなく、yにundefinedが入ったオブジェクトに変わっている
- うーん、これは「メンバが存在しないときとundefinedが入ってときとで挙動が違うライブラリ」を使ってる時に厄介ごとが起きそうだ…
    - 有名どころだとFirebase Cloud Firestoreはシリアライズ時に`undefined`が入ってると例外を投げる
    - このページの本題と違うけどFirestoreに関しては2020年5月の更新でundefinedを無視するオプションが増えてることに気づいた。つけとこ。
        - > Whether to skip nested properties that are set to undefined during object serialization.  If set to `true`, these properties are skipped and not written to Firestore. If set to `false` or omitted, the SDK throws an exception when it encounters properties of type `undefined`. [doc](https://firebase.google.com/docs/reference/js/v8/firebase.firestore.Settings?hl=ja#optional-ignoreundefinedproperties)

ts

```typescript
const input_object = { x: 1 };
const tmp = IO_OpeionalY.decode(input_object);
let value4: OptionalY;
if (isRight(tmp)) {
  value4 = tmp.right;
} else {
  throw new Error();
}
expect(JSON.stringify(value4)).toBe(`{"x":1}`);
expect(value4).toEqual(input_object);
// expect(Object.entries(value4)).toEqual(Object.entries(input_object));  // fail
```


