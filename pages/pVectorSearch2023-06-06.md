
prev [[pVectorSearch2023-06-05]]

Firebaseに検索結果を保存し、それをシェアするためのパーマリンクを作る
- `$ npm install firebase`
- ![image](https://gyazo.com/82af3a39197d8eb14dd5749d40371f6f/thumb/1000)
    - ほー、新しい書き方が生まれてる
    - ChatGPTに新しい書き方の方を使って、と言ったらわかってくれるかな？
        - 自分で新しい書き方に書き換えてしまった
- NextJSでURLからIDを取得して表示して？と言ったら書いてくれた
    - `pages/result/[id].js`
    - TypeScriptと指定し忘れてJSで書かれた
    - コンパイル通ったのに404だけど？と聞いたらチェックリストを出してくれた
    - パスあってるか確認して？と言われたので確認したら`app/pages/result/[id].tsx`に置いてたw
        - 人間がやりがちな典型的なミスのことを知ってるw

リリースした: [[西尾のベクトル検索]]

ページタイトル画像
- `/api/pages/:projectName/:pageTitle/icon`
- ✅表示できた

- 管理者用の画面
    - 検索クエリは保管して管理者が見れるようにする
        - ✅そういう旨の説明が書いてあるページを作る
        - ✅検索した時点で結果をFirebaseに入れてパーマリンクを出すか
    - ✅公開する
    - ❎[[URL Fragment Text Directives]]をつける
        - これ厄介だな
            - 例えばScrapbox記法が混じってるとブラウザのテキストには記法がないからヒットしない
            - 真面目にやるならプレーンテキストにする必要がある
        - いや、これ新しいページを開いたときにはScrapbox側が行IDだと仮定して取っちゃって本来の挙動が発動しないのでは
        - コメントアウトした
            - Scrapboxがダメ？なだけなので他のサービスだと使えるかも知れない
- 管理者(や特別に許可された人)かどうかでUIを変える
    - [GitHub - firebase/firebaseui-web: FirebaseUI is an open-source JavaScript library for Web that provides simple, customizable UI bindings on top of Firebase SDKs to eliminate boilerplate code and promote best practices.](https://github.com/firebase/firebaseui-web)
    - `$ npm install firebase firebaseui --save`
- ![image](https://gyazo.com/4f694f09f47ddd2ee50ae33b078e56c9/thumb/1000)
    - 見た目はさておき管理ページができた
ts

```typescript
 let list = null;
 if (user.email === "nishio.hirokazu@gmail.com") {
   list = QueryList();
 }
 return (
   <>
     <div>Welcome, {user.displayName}!</div>
     {list}
   </>
 );
```

- こんな感じなので特定機能だけ特定の知り合いに許可するのもできる
- ちょうど話す機会があったのでこれを作った話をしてhal_skとyuisekiから検索対象にする許諾をもらった
- ネクストアクションはエクスポートを介さずに公開プロジェクトのデータを吸い取ってインデックスにすること
    - 井戸端バックアッププロジェクトのコードでできるはず

[GPT](https://chat.openai.com/share/50048950-c6f4-414b-b941-d26c2b1e235a)
next [[pVectorSearch2023-06-07]]
