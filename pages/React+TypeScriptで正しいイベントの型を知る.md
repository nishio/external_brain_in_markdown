
イベントの型を正しく付けることは大事なのだけど、何が正しい型なのかわからなくて雑に付けてしまいがち(過去の自分の失敗談)
正しいイベントの型を覚えたりする必要はなくて「明らかに正しくないvoidなどの型にして、TypeScriptが正解を教えてくれるのでそれを使う」ってだけで良い。
![image](https://gyazo.com/b69ada33003d39d9ef432c8a51b40987/thumb/1000)

文脈
> [qnighy](https://twitter.com/qnighy/status/1416745698918244356) e.​target間違って使われがち問題
>  ![image](https://gyazo.com/afa6e2820782a7cef3293d9afb83dc32/thumb/1000)

[nishio](https://twitter.com/nishio/status/1416805618686435328) これ最近fooに直接eを渡した上で補完候補見て「ん？currentTarget？知らない子だな、でも期待した型がついてるからこれでいいか、後で調べよ」と思って調べてなかったことを思い出した。
ts

```typescript
const onDragStart = (event: React.DragEvent<HTMLDivElement>) => {
    event.target.clientHeight // あれ？ないな？
    event.currentTarget // これか
```

という流れ

型情報
`event.target: EventTarget`
`event.currentTarget: EventTarget & HTMLDivElement`

MDN
- [Event.currentTarget](https://developer.mozilla.org/ja/docs/Web/API/Event/currentTarget)
    - > イベントは DOM を横断するので、イベントの現在のターゲットを識別します。イベントが発生した要素を特定する event.target とは対照的に、常にイベントハンドラがアタッチされた要素を参照します。
- [Event.target](https://developer.mozilla.org/ja/docs/Web/API/Event/target)
    - > イベントを発生させたオブジェクトへの参照です。 イベントハンドラーがバブリング、またはキャプチャフェーズの間に呼び出されたとき、event.currentTarget とは異なります。

あー、なるほど。targetは子要素のどれにもなり得るがcurrentTargetはイベントハンドラのついてるDOM要素になるわけか。だから`event: React.DragEvent<HTMLDivElement>`の型引数による「`HTMLDivElement`だ」って情報が、targetには影響せずcurrentTargetにはついたわけね

これって「eventの型を正しく付けていることによって無意識に落とし穴から守られた」ということなのだけど、最初にTypeScript+Reactで見様見真似でプロトタイプ作った時はeventの型を正しくつけてなかったと思う。
implicit anyだと警告されて明示的にanyにしたりevent: Eventってしたり。
![image](https://gyazo.com/db8b07cad53478a411b439df60485031/thumb/1000)

「implicit any」になるということはつまり「型情報が推測できないから人間がきちんとつけてね、変なのつけても検知できないよ」ということであり、実は一番きちんとやらなきゃいけないところなのに、雑に型をつけてしまい、その結果イベントハンドラの中身の実装で型の支援が得られなかったりする
ts

```typescript
  const onDragStart = (event: Event /* NG: 適切な型ではないが警告されない */) => {
    console.log(event.currentTarget.clientHeight); // ここでエラーになる
    // Object is possibly 'null'.  Event.currentTarget: EventTarget | null
    // Property 'clientHeight' does not exist on type 'EventTarget'.
  };
```


React+TypeScriptで正しいイベントの型を知る(このページ)
このテクニックに気づいてから正しい型をつけることが楽チンになったのだけど、こういうことってどこで学ぶのか。

[[TypeScript]]
[[React]]
