
デバッグ目的で変数dbを露出させたくて`window.db = db;`したら「windowはそんなプロパティ持ってないよ」と言われる。
Quick Fixでdeclareできそうだったのでやってみたらlib.dom.d.tsの中のinterface Windowの定義に db : any が追加された。これは絶対に後で戻すのを忘れるのでいやだ。
TypeScriptにおいて宣言はだいたいマージされる。だから直接編集しなくてもこれで良い:
typescript

```typescript
declare global {
    interface Window { db: any; }
}
window.db = db;
```


このglobalはは[[Module Augmentation]]の一種、Global augmentationだ。see [Declaration Merging · TypeScript](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)

typescript

```typescript
declare module "./modulename" {
    interface Foo { Bar: Baz; }
}
```


「この宣言が書かれているモジュールで新しいWindowを定義するんじゃなくて、グローバルのWindowに対してマージせよ」という意味でglobalがついている。
