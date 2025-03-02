
en [https://basarat.gitbook.io/typescript/type-system/index-signatures#using-a-limited-set-of-string-literals](https://basarat.gitbook.io/typescript/type-system/index-signatures#using-a-limited-set-of-string-literals)
ja [https://typescript-jp.gitbook.io/deep-dive/type-system/index-signatures#riteraruwosuru](https://typescript-jp.gitbook.io/deep-dive/type-system/index-signatures#riteraruwosuru)
Using a limited set of string literals
限られた個数の文字列リテラルを使う
An index signature can require that index strings be members of a union of literal strings by using Mapped Types e.g.:
マップ型を使うことで、インデックス文字列が「リテラル文字型のユニオン型」のメンバであることを要求するようなインデックスシグニチャを作ることができます。

This is often used together with keyof typeof to capture vocabulary types, described on the next page.
辞書の語彙の型を得るために、次のページで解説するkeyof typeofがしばしば共に使われます。
The specification of the vocabulary can be deferred generically:
語彙の指定はジェネリクスを使うことで後回しにできます。


ts

```typescript
type K = "A" | "B" | "C";
const x1: { [k in K]: number } = { A: 1, B: 2, C: 3 }; // OK
// const x2: { [k in K]: number } = { A: 1, B: 2 }; // NG: Property 'C' is missing
const x3: { [k in K]?: number } = { A: 1, B: 2 }; // OK
// const x4: { [k in K]: number } = { A: 1, B: 2, C: 3, D: 4 };
// NG: Object literal may only specify known properties, and 'D' does not exist
```


