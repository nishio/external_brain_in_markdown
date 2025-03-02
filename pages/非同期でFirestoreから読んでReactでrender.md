
[[React勉強日記]]

[[Firestore]]のリアルタイム更新リスナを登録して、更新があった時に[[React]]で再renderをしたい。
リアルタイム更新をリスンするかどうかにかかわらず、読み出しAPIはプロミスを返すので非同期。
Reactは状態更新のタイミングで再描画をするのでこれを使う。
結果: Firestore上の値が変わるとブラウザ上の表示も自動的に変わるプロトタイプができた

つまずきポイント
- React.Componentは型関数で、第二型引数としてstateの型を取る
    - 与えなかった場合は`{}`が与えられたものとして動く
        - 定義: `interface Component<P = {}, S = {}, SS = any>`
    - その結果`this.state.pieces`に対して「Readonly<{}>はpiecesを持たない」ってなる
    - Property 'pieces' does not exist on type 'Readonly<{}>'.

- FirebaseのサンプルではonSnapshotの引数にfunctionを使っているが、このままだとComponentのthisをshadowする
    - Visual Studio Codeが警告してくれたのでそこにはハマらなかった
    - だがこの問題の解決方法を僕が正しく理解していなかった
    - thisがshadowされてアクセスできなくなるので
    - 外のスコープで`let setState = this.setState`してこれを使えば良いだろうと考えた
        - Python的発想。Pythonはオブジェクトのメソッドはオブジェクトにバインドされている
        - JSではそんなことはない。this.setStateは単なる関数
        - その結果 TypeError: Cannot read property 'updater' of undefined
            - [TypeError: Cannot read property 'updater' of undefined · Issue #9654 · facebook/react](https://github.com/facebook/react/issues/9654)
            - [エラーで学ぶReactJS - くろのて](http://note.crohaco.net/2018/react-errors-warnings/)
    - かつてのJSでは明示的にバインドすることで解決する
        - `const setState = this.setState.bind(this)`
    - 今時のES6ではアロー関数が呼び出し時にthisをbindしない(のでshadowしない)ことを使うことができる
        - 今回はこれを使った
        - > An arrow function expression is a syntactically compact alternative to a regular function expression, although without its own bindings to the this, arguments, super, or new.target keywords.
        - [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

疑問点
- 僕はconstructorを使ったが、[[componentDidMount]]を使っている人がちらほらいる。何が違うのか。

typescript

```typescript
class App extends React.Component<{}, { pieces: any[] }> {
  constructor(props: {}) {
    super(props);
    this.state = { pieces: [] };
    db.collection("pieces").onSnapshot((querySnapshot: any) => {
      let pieces: any[] = [];
      querySnapshot.forEach(function (doc: any) {
        pieces.push(doc.data().text);
      });
      this.setState({ pieces: pieces });
    });
  }
  render() {
    let pieces = this.state.pieces.map((x) => <SimplePiece text={x}></SimplePiece>);
    return (
      <div className="App">
        <header className="App-header">
          {pieces}
        </header>
      </div>
    );
  }
}
```


