---
title: "2021-08-02Movidea/Kozaneba開発日記"
---

Windowsのユーザ
- 4 本指ジェスチャーまで認識するタイプのタッチパッド
- 操作できるか？
不確実なものほど素早く検証するべき
- 認証とクラウド保存は一旦脇に置いて、操作できるのかどうかの検証をするべき
- そのためには
    - デプロイをする
    - Movideaで行くか、落ち着いたら変えようと思ってたKozanebaに今変えるか
        - [[2021-07-15Movidea開発日記#60effb2baff09e00003b7dcd]]
        - リポジトリやNetlifyの設定を後からまた変えるのは二度手間なので今Kozanebaにする
        - ソースやタイトルバーなどは後ほど変える
    - 操作できるかのテストのための小さいサンプルを作る
        - [https://kozaneba.netlify.app/#tinysample](https://kozaneba.netlify.app/#tinysample)
    - 二本指ジェスチャーで操作してるところを動画に撮ってみた
        - [https://youtu.be/FvZvZ1jVKrk](https://youtu.be/FvZvZ1jVKrk)
- WindowsのChromeでは最初に垂直または水平に動かした時にその方向の移動にロックされる振る舞いがある
    - 980479 - two-finger trackpad movement locks in as horizontal or vertical - chromium
    - [https://bugs.chromium.org/p/chromium/issues/detail?id=980479](https://bugs.chromium.org/p/chromium/issues/detail?id=980479)


認証
- 匿名認証
    - ![image](https://gyazo.com/85e7eba0fd4c3bd40818c6694c063ec9/thumb/1000)

[JavaScript を使用して Firebase 匿名認証を行う](https://firebase.google.com/docs/auth/web/anonymous-auth?hl=ja)
- > 匿名アカウントを永久アカウントに変換する
- >  匿名ユーザーがアプリへ登録した後、新しいアカウントの下で引き続き従来の作業を行えるようにしなければならない場合があります。たとえば、アプリへの登録前にユーザーがショッピング カートに追加したアイテムを、新しいアカウントのショッピング カートにも入れておく、といったケースです。手順は次のとおりです。
- >  ...
- > link の呼び出しが成功したら、ユーザーの新しいアカウントが匿名アカウントの Firebase データにアクセスできるようになります。
- リンクしたらuser.uidが同一になるのかな
    - [JavaScript を使用してアカウントに複数の認証プロバイダをリンクする | Firebase](https://firebase.google.com/docs/auth/web/account-linking?hl=ja)
    - > ログインに使用した認証プロバイダに関係なく、同じ Firebase ユーザー ID でユーザーを識別できます。
    - はー、なるほど。ユーザと認証プロバイダが1対他の対応になってるわけか

[認証状態の永続性 | Firebase](https://firebase.google.com/docs/auth/web/auth-state-persistence?hl=ja)
- デフォルトでログインしっぱなしになるみたい、それでいい

とりあえず「現在のユーザ: null」まではできた
- ✅匿名でログインして、ブラウザをリロードしてもログイン済み
- ログアウトのメニューを作らねば
- ✅ログアウトして再度匿名ログインしたら別のuidになる
- ✅Google OAuth
    - ![image](https://gyazo.com/c22edbc879ea0a5937af97351b2b59be/thumb/1000)
        - [Showing a custom domain during sign in](https://cloud.google.com/identity-platform/docs/show-custom-domain)
            - [Connect a custom domain | Firebase](https://firebase.google.com/docs/hosting/custom-domain)

コンソール
- ![image](https://gyazo.com/582157f59c7c6dad53f159fa3b8e7d98/thumb/1000)
- はー、なるほど、こうなるのか

ts

```typescript
import "firebaseui";
var ui = new firebaseui.auth.AuthUI(firebase.auth());
// 'firebaseui' refers to a UMD global, but the current file is a module. Consider adding an import instead. ts(2686)
```

ts

```typescript
import firebaseui from "firebaseui";
// Attempted import error: 'firebaseui' does not contain a default export (imported as 'firebaseui').
```

ts

```typescript
import * as firebaseui from "firebaseui";
// Import may be converted to a default import. ts(80003)
```

![image](https://gyazo.com/f20f0b9ebab31b694a6f6233970dbcb5/thumb/1000)

html

```html
<link type="text/css" rel="stylesheet" href="https://www.gstatic.com/firebasejs/ui/4.8.1/firebase-ui-auth.css" />
```

![image](https://gyazo.com/4d92cd515b20dd245b8910bb42c81ccf/thumb/1000)

[https://www.npmjs.com/package/identicon](https://www.npmjs.com/package/identicon)

だいぶ部品が揃ったので改めて考える

再掲
- 絶対にダメなこと
    - チュートリアル開始前にログインを要求する
    - 閲覧オンリーで渡したURLから編集権限が得られること
- 好まないこと
    - 一人で使っててHandoffで渡した時に渡した先でログインが必要になること
        - ログインが一回だけで、セッションが長く続くなら許容範囲か

デフォルトではURLを知っていればアクセスできる
- 後からアクセス権を絞れる
    - writeを特定のユーザに限定するとか
    - リードオンリーのリンクを作るとか
        - これはすなわち作者一人にwriteを制限することと同じ
    - この「アクセス権の変更権」をオーナーだけに持たせる
        - ここでオーナー識別のためにログインしてなくても匿名ユーザを作る？
        - それともクラウド保存をするためにはログインが必要とする？
            - それはおかしな設計ではない、よくある
            - 一方でアカウントがないと使い始められないのはイマイチに感じる？
                - メールとパスワードでアカウントを作るのではなくOAuthだからそれほど気にすることでもない？

アクセス権を絞るタイミングでは必要なのだけど、それより手前のクラウド保存するタイミングで「ログインしてね」って言われるのが自然かなぁ
- で、その段階ではアクセス権を絞ってないのでHandoffしたら書き込める
- その後、リードオンリービューを作ってシェアしようとしたら書き込めてた端末が書き込めなくなっちゃう…と思ったけど、writerを記録しておいてリードオンリービューを作る時にオーナーに絞るのではなく既存のwriterに絞ればいいのでは
- Handoffで渡された端末は匿名ログインして自分のユーザIDをwriterに書き込む
    - これで「今書き込みモードで接続してる人数の可視化」もできる
