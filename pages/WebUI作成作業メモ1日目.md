
from [[WebUI作成作業メモ]]
- `$ npx create-react-app keicho-webclient --template typescript`
    - [[create-react-app]]
    - `--typescript`ではダメになったっぽい
- [[reportWebVitals]]ってのが新しく増えてる
- ルーティングは一旦置いといてメインの画面を作ってみる
    - 前回Appなら書いて行ったら肥大化してしまったので気をつける
- [[Material-UI]]
    - `$ npm install @material-ui/icons`
    - AppBar
        - ![image](https://gyazo.com/62a1e988dfad4221136ab2c511f7c8d1/thumb/1000)

    - [[nisbot]]

- [[チャット CSS]]
    - [HTMLとCSSでLINE風チャット画面(会話方式)を記事に表示する方法(ほんとに売ってるラインスタンプイラスト41個付き) | ナコさんのブログ | nako-log](https://nakox.jp/web/coding/chat_line_css)
    - `To import Sass files, you first need to install node-sass`
    - `$ npm install node-sass`
    - `Error: Node Sass version 5.0.0 is incompatible with ^4.0.0.`
    - `$ npm install node-sass@4`
    - ![image](https://gyazo.com/eee5a71e72b876bcd337ef628ebdea3b/thumb/1000)
- ![image](https://gyazo.com/fe2db5ea616df69c9278731d91291575/thumb/1000)
- ![image](https://gyazo.com/935fc3a9900b74d9bfee6f495941bc56/thumb/1000)
- チャット部分はコンポーネントに切り分けた
- 後で検討: 投稿の間の隙間が異なるの気になる
- 後で検討: ボットの発言だけコンテンツより長く伸びる
    - ![image](https://gyazo.com/4afe81b382d97816b4010ebe489a6eb1/thumb/1000)


Githubに置いてNetlifyでデプロイする
- Netlifyのウィザードに従うだけ
- バッジを貼ってみた
- ![image](https://gyazo.com/a94c447f431e167c874b1fcc8d5f0510/thumb/1000)



次にやること
- スマホで開くと文字が小さいときはズームしてしまう
    - 直した
    - ![image](https://gyazo.com/07cce875ba995cb4ed0d7c3d656f46bf/thumb/1000)
    - ボットの発言だけ伸びるのも嫌だったので全部伸ばしてみた

- テキストエリアでの改行で発言追加
    - ![image](https://gyazo.com/b217f31537d832458e4216eddfc0b3b1/thumb/1000)
        - word-break: break-all;することにした(日本語ユーザなので)
- テキストエリアでの改行でサーバを叩く
    - [[Flask-CORS]]
    - 400 Bad Requestになった→[[JSからFlaskを叩いて400 Bad Request]]
- レスポンスを表示する
    - とりあえずnopを返すようにして、無事表示できた
    - ![image](https://gyazo.com/6fb9804c98e4fdbd44c2ee5ffd949259/thumb/1000)
- ページを開いた時点で新しいenvオブジェクトを作るようにする
    - env作成APIが必要
    - 新規作成してIDを返す
    - サーバをいじるとき、いちいちデプロイしないでローカルで試したい
        - [[FlaskをHTTPSにする]]
        - 必要なかった
- 動くようになった
    - ローカル
        - ![image](https://gyazo.com/8b13f63872d28ec0d8caa502f21e399b/thumb/1000)
    - サーバー
        - ![image](https://gyazo.com/2703587bc408d7c3c5157aacbee267e7/thumb/1000)
- ローカルとかサーバーとかの表現が微妙なので整理した
    - ![image](https://gyazo.com/032a384998c7547e0048897b9549e552/thumb/1000)
    - 上記のスクショはTypeScriptのクライアントをローカルとリモートと両方で試して問題なく動いたって話
    - 後者は開発用PCではなくスマホからアクセスしている

次にやること
- ログが表示できるようにする
    - Regroupにインポートしたり、Scrapboxに貼ったり
- テストできるようにする
    - たぶん内部構造を少しいじりたくなると思うのだけど、テストなしでいじると地獄だから
        - 学習データにするためや、Regroupにインポートするためにいじりたい
- Firebaseに溜まったデータをローカルにダウンロードして解析できるようにする
- どれをやるのか相談してみた
    - [[会話ログ20210120]]
    - Regroupにインポートできる形でのログ出力が大事
