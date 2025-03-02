
[[TypeScriptの型]]
> TypeScriptの型の情報で例えば「英数字のみからなるidを持つ」って定義できる？ [src](https://twitter.com/wtnabe/status/1252119742069891073)
ってのを見て、そういえばどうやるんだろうなと思って調べたのでメモ

この種のニーズって要するに[[構造的型付け]]のTypeScriptにおいて、データの構造としては既存のStringを使いつつ、値の範囲を制限して、その値の集合に別の名前をつけたい、Nominal Typingしたい、ということかと思う。

Nominal Typingで調べたらすぐ見つかった。
[Nominal Typing - TypeScript Deep Dive](https://basarat.gitbook.io/typescript/main-1/nominaltyping)

簡単に言えば型の区別のためのメンバを導入して構造的な互換性をなくせば良い、というシンプルなもの。
この解説を参考にして、奇数の型を作ってみた。

ts

```typescript
interface Odd extends Number {
  _OddBrand: boolean;
}
interface Even extends Number {
  _EvenBrand: boolean;
}

var odd: Odd;
var even: Even;

// Expected Type Errors
// odd = even;  // NG
// even = odd;  // NG
// odd = 1;  // NG

const assertOdd = (x: number): Odd => {
  if (x % 2 === 1) {
    // @ts-ignore
    x._oddBrand = true;
    // @ts-ignore
    const ret: Odd = x;
    return ret;
  }
  throw AssertionError;
};

var x = assertOdd(1);
odd = x;  // OK
// even = x;  // NG
```


人によっては「期待よりも厳しい」と感じるかも。
`odd = 1`は型エラーになる。
この例のように「number型だが、奇数であるの明らかだ」と思うならassertすれば良い。
このassertが間違っていた時には実行時にアサーションエラーになる。
