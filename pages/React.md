---
title: "React"
---

- [https://reactjs.org/tutorial/tutorial.html](https://reactjs.org/tutorial/tutorial.html)
- [https://reactjs.org/docs/hello-world.html](https://reactjs.org/docs/hello-world.html)
- [[Builderscon 2018]]での講演スライド
    - [https://speakerdeck.com/koba04/algorithms-in-react](https://speakerdeck.com/koba04/algorithms-in-react)
        - Reactはトラバースをかつて再帰呼び出しで実装していた
            - 再帰呼び出しは中断できない
            - そのため、大きくなった時にUIをブロックする
            - だから最近のReactではファイバーを使って中断可能にしてる
    - 昔の実装にどういう問題があって、だからどう変更したのか、それによってライブラリのユーザがどのように書き方を変えなければならなかったか(状態更新の非同期化とか)が解説されてとても良い
    - 副作用の優先度の話
        - ユーザー入力イベントはハイプライオリティになっている
        - だからそこで重い処理をすると入力がブロックされてユーザが不快
        - ロープライオリティに切り出してやることでユーザの入力は快適になる
        - エクスパイアの時に同期的に実行される
    - サスペンス
        - エラーバウンダリーと類似の仕組み
        - エラーを投げる代わりにプロミスを投げる
        - ライブラリ内部で即座にキャッチされて親リンクを非同期にたどっていく
        - 時間がかかった時だけローディング出したりできる
        - 面白いしユーザのストレスを減らすのにとても重要そうだけど、まだあまり枯れてなさそう

既存のプロジェクトを部分的にReact化する
新しいものを作る時もこのテンプレから始めるので良さそう
[https://reactjs.org/docs/add-react-to-a-website.html](https://reactjs.org/docs/add-react-to-a-website.html)

ツールチェーンの構築は、必要性を感じてから（十分複雑になってから）やる
[https://reactjs.org/docs/create-a-new-react-app.html](https://reactjs.org/docs/create-a-new-react-app.html)

onClickはhandleClickで受ける
[https://reactjs.org/docs/handling-events.html](https://reactjs.org/docs/handling-events.html)

Props are read-only
[https://reactjs.org/docs/components-and-props.html#props-are-read-only](https://reactjs.org/docs/components-and-props.html#props-are-read-only)
なるほど、モデルとビューの分離か
stateの更新はthis.setStateに、前のstateを引数として取って新しいstateを作って返す関数を渡す

「クリックすると色が変わる丸」というコンポーネント
[https://codepen.io/nishiohirokazu/pen/YOWqKw](https://codepen.io/nishiohirokazu/pen/YOWqKw)

自分で開発環境を作らなくてもブラウザ上で色々できすぎて、逆に自分で開発環境を作るのがめんどくさいと思ってしまうが、とはいえブラウザ上だけでずっと開発するのもそれはそれで辛い。仕方ない。
[https://reactjs.org/tutorial/tutorial.html#setup-option-2-local-development-environment](https://reactjs.org/tutorial/tutorial.html#setup-option-2-local-development-environment)


With SVG
- [https://auth0.com/blog/developing-games-with-react-redux-and-svg-part-1/](https://auth0.com/blog/developing-games-with-react-redux-and-svg-part-1/)
- [https://medium.com/@ericschwartz7/using-react-with-svg-57958f16e68a](https://medium.com/@ericschwartz7/using-react-with-svg-57958f16e68a)

JSコード中にHTML的なものを書くJSX
- `<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>`
- Babelで変換

- [https://github.com/tanem/react-svg](https://github.com/tanem/react-svg)
    - これはSVGファイルを入れるためのものっぽい

- [http://youmightnotneedjquery.com/](http://youmightnotneedjquery.com/)

js

```javascript
const e = React.createElement;

class LikeButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = { liked: false };
  }

  render() {
    if (this.state.liked) {
      return 'You liked this.';
    }

    return e(
      'button',
      { onClick: () => this.setState({ liked: true }) },
      'Like'
    );
  }
}

ReactDOM.render(
    e(LikeButton),
    document.getElementById('root')
);
console.log('OK')
```

[https://reactjs.org/docs/add-react-to-a-website.html](https://reactjs.org/docs/add-react-to-a-website.html)

:

```
<svg width="100" height="100"　id="canvas">
<circle cx="50" cy="50" r="40" stroke="green" strokeWidth="4" fill="yellow" />
  </svg>
```



js

```javascript
  handleClick(e) {
    console.log("clicked");
    this.setState(prevState => {
      console.log(prevState);
      return {
        value: !prevState.value
      };
    });
  }

```

