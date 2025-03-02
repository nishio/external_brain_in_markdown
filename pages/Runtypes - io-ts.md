
> [whitphx_ja:](https://twitter.com/whitphx_ja/status/1436946766167826437) Runtypes推し
- >  型定義がそのまま型チェッカの実装にもなって楽なので
- >  interfaceが増えてきたり複雑なinterfaceが登場したりしたらいちいち自分でチェッカを書いていられない
    - [https://github.com/pelotom/runtypes](https://github.com/pelotom/runtypes)
- > io-tsの方がstar多いけど、関数型の匂いが強すぎてよわよわな自分には合わなかった
    - [https://github.com/gcanti/io-ts](https://github.com/gcanti/io-ts)

自分でJSONの型チェックするコードを書いてしまったが、自動化できるのか。
人間が書くとバグるからこれを使う方向に進むか〜

Runtypes / io-tsのどっちを使うか、小さい(けど自分の使う複雑な構造を含んだ)型を使って比較する

ts

```typescript
test("io-ts, use implemented type", () => {
  const obj_string = JSON.parse(`"hello"`); // is any
  const obj_number = JSON.parse(`123`); // is any

  expect(isRight(t.string.decode(obj_string))).toBeTruthy();
  expect(isRight(t.string.decode(obj_number))).toBeFalsy();

  const ret = t.string.decode(obj_string);
  let string_value: string;
  if (isRight(ret)) {
    string_value = ret.right;
  } else {
    throw new Error("not string");
  }
  expect(string_value).toBe("hello");
});

test("runtypes, use implemented type", () => {
  const obj_string = JSON.parse(`"hello"`); // is any
  const obj_number = JSON.parse(`123`); // is any

  expect(String.guard(obj_string)).toBeTruthy();
  expect(String.guard(obj_number)).toBeFalsy();

  let string_value: string;
  if (String.guard(obj_string)) {
    string_value = obj_string;
  } else {
    throw new Error("not string");
  }
  expect(string_value).toBe("hello");
});
```


現実の「複雑な型」をio-tsとruntypesで書き比べ
- [https://gist.github.com/nishio/a5f8bdbc7961f3c0a569653e2dacfdd3](https://gist.github.com/nishio/a5f8bdbc7961f3c0a569653e2dacfdd3)
- どちらのライブラリも2時間前に同時にインストールしたばかりの経験ゼロなので、同等にポンコツだと思って良い。
- 疑問点1: io-ts、optionalのサポートがなくてpartialとのintersectionを作れとか書いてあるけど、ほんとにそれでいいの？振る舞いとしては同じだけど生成される型は酷い見た目だよ？
- 疑問点2: runtypesでio-tsのrecord相当のことをする方法がドキュメントを見てもよくわからない。自明だと思ったのかなのか省略されてる。(runtypesのRecordはio-tsのtypeなので別物)
    - キーがBrandedである場合、というこれまた現実によくあるやつの解決方法を参考にしたが、あってるかわからない。
    - 実際に僕の書いてるやつでもキーはBrandedなのだが、JSONから読んだもののチェックをする目的で使おうと思ってるのでその段階ではstringでいいやーとなってる。Branded typesはどちらでも明示的にサポートしてる。
- runtypesの側はPattern matchingの章に書かれてる通りunion型に対するそれぞれの型のための処理を関数オーバーロード的に一つに束ねて書ける。「へー、面白いじゃん」的な感じ。
- runtypesは通常の型チェックではできないような「正の数」なども「Numberに、正である制約をつけたもの」として型オブジェクトにすることができる。もちろん型にした時には制約が外れたnumberになるが、型ガードではちゃんとチェックされる。
    - runtypesでは、関数に契約をつけることができる。例えばゼロになってはいけない制約をつけることができる。この時の書き方はコンパクトではあるが、ちょっとabuseっぽさがある。言語内DSLで英文法に寄せてる感じがある。
- io-tsは裸のEither型を返してくるのでギョッとする人も多いかもしれない。内部構造もろだし感。
    - だけどまぁ現実の利用の際には自分で好きなようにラップすれば良いだろうとも思う。中身が出てるから扱いやすくなることもあると思う。runtypesでどうなってるのかは知らない。
    - 例えば「これからTypeScriptでプログラミング言語を実装します」という場合だったら、どこでどんなエラーが起きたとか何件起きたなどを取得できるio-tsの方が向いてるかも。
    - 一方で僕は「壊れてないはずのJSONを読むが、壊れてた時に素通しすると問題究明しにくいから読むタイミングでチェックしたい」程度のことなので、まあruntypesの方が向いてそうかなと思う。
        - io-tsでも自分の好むインターフェースになるようにユーティリティ関数を実装すれば良い、そこまで労力かける気がないってだけ

io-tsのoptional型に対する対処法が気持ち悪すぎる
- 逆にまあ「optional型なんて気持ち悪いもの使わねえよ」と言い切れるようなケースでならio-tsはフィットすると思う。これは結局のところ型との付き合い方のスタンスの違いだと思う。
- > [odiak_](https://twitter.com/odiak_/status/1438822559290589186): `const optional=(tp)=>t.union([tp, t.undefined])`というようなやつを定義して、`t.type({a: optional(t.string),b:t.number})`などと書くと良いと思います。これは`{a?: string, b: number}`とは厳密には違うんですが、`{b: 3}`のような値も受け付けてくれて実用上問題ないです。

- [[Runtypes と io-ts のoptionalの比較]]

> [odiak_](https://twitter.com/odiak_/status/1438823161064091651): あと、io-tsはcustom typeを定義すると色々やれて楽しいです。値に制約を付けた型や、特定のオブジェクトに変換する型、T|null|undefinedをT|undefinedに変換する型など。

Runtypesにcheckってメソッドがある
- before
ts

```typescript
let string_value: string;
if (String.guard(obj_string)) {
  string_value = obj_string;
} else {
  throw new Error("not string");
}
```

- after
ts

```typescript
  {
    const string_value = String.check(obj_string);
    expect(string_value).toBe("hello");
  }
  // const string_value = String.check(obj_number);
  // throws: `ValidationError: Expected string, but was number`
```

- 親切なエラーメッセージだ
