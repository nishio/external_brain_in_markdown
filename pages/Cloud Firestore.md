
[[Regroup]]のバックエンド
- 旧KJ法ツールでは[[Google Realtime API]]を使っていたが2019年1月に終了予定
- [[Firebase]]にしようかなと思って調査したらCloud [[Firestore]]がベータリリースしてた
    - データモデル的にしっくり来そうなのでこっちにすることにした
- Scrapboxをバックエンドにする案はやめた
    - Scrapboxはやはり人間とのインターフェイスであって、機械的なデータを置くべきではない
    - [[Scrapboxからのインポート]]はできるようにする予定

- 「コレクション」の中に「ドキュメント」がある仕組み
    - ドキュメントはJSONだと思えば良い(+データ型がいくつか追加されてる)
    - ドキュメントは1MBまで
    - ドキュメントの中にまたコレクションを入れることはできる

- [サポートされているデータ型  |  Firebase](https://firebase.google.com/docs/firestore/manage-data/data-types?hl=ja)
    - ドキュメントの中にマップや配列、参照が入れられる
    - テキスト
        - > UTF-8 表現の最初の 1,500 バイトのみがクエリによって考慮されます。
        - 単独フィールドに対するインデックスは自動で生成されるが長文テキストはインデックスが無意味なので明示的に除外したほうがよい（課金的な意味で）

- doc("...").set(...)で上書き(なければ作成)
    - merge: trueを指定するとマージ [ref](https://firebase.google.com/docs/firestore/manage-data/add-data?hl=ja)
    - collectionsRef.doc("hoge").set(...)でID指定で作成できる
    - collectionRef.add(...)でID自動生成で追加できる
        - ref = collections.doc() してから ref.set(data)が良さそう
        - {timestamp: firebase.firestore.FieldValue.serverTimestamp()}を入れておくと良さげ
            - オフラインで書くことがあるからcreatedは手元のタイムスタンプを入れたほうが良さげ
    - 書き込み命令はPromiseを返して、完了時にthenが呼ばれる
        - オフラインで書き込みをするとオンラインに戻ってサーバに書き込めた時点でthenが呼ばれる
        - なのでこれをウォッチして「書き込み済み」マークを表示するのが良さそう
        - それと別にsnapshot.metadata.hasPendingWritesで未完了の書き込みの有無がわかる
            - [Cloud Firestore でリアルタイム アップデートを入手する  |  Firebase](https://firebase.google.com/docs/firestore/query-data/listen)
    - docRef.updateもあるぞ？merge:trueと何が違うんだ？
- 存在しないドキュメントをgetしてもエラーにはならない
    - 空のオブジェクトが帰ってくる
    - doc.exists() => false
- `.onSnapshot(function(querySnapshot) {`
    - 更新をlistenする
- 一括書き込み [src](https://firebase.google.com/docs/firestore/manage-data/transactions)
    - 一度に500件
    - batch = db.batch()に対して操作をしてからbatch.commit()

- [全文検索  |  Firebase](https://firebase.google.com/docs/firestore/solutions/search?hl=ja)

- オフラインの永続性
    - [オフライン データを有効にする  |  Firebase](https://firebase.google.com/docs/firestore/manage-data/enable-offline)
    - > ユーザーが同じ Cloud Firestore データベースを参照する複数のブラウザタブを開き、オフラインの永続性が有効になっている場合、Cloud Firestore は最初のタブでのみ正しく動作します。
    - それはうっかりミスで複数タブ開いてデータをとばしそうで怖いな
    - サンプルコードを見ると一応検出できるっぽいので、ユーザに警告すべきだな
    - Wifiを切って書き込んだものがWifi再接続後にサーバに保存されるのを確認した
        - 接続があってもなくてもsnapshot.metadataはfromCache: false
        - 一方でブラウザをリロードした時にはfromCache: trueである

- Python API
    - [Cloud Firestore を使ってみる  |  Firebase](https://firebase.google.com/docs/firestore/quickstart) のPythonのところを見る
    - `cred = credentials.ApplicationDefault()`が成功するためには [認証の開始  |  認証  |  Google Cloud](https://cloud.google.com/docs/authentication/getting-started) を読んでJSONのダウンロードと環境変数の設定が必要
    - Pythonでは`collection.doc()`ではなく`collection.document()`
    - DocRef#getは`document.DocumentSnapshot`を返す
        - .to_dict()で辞書になる
    - `db.collection("...").get()`が「すべてのドキュメントを返す」と書いてあって、マジかと思ったがジェネレータが作成されるので安心
        - `DeprecationWarning: 'Collection.get' is deprecated:  please use 'Collection.stream' instead.`
        - `xs.__next__() # => document.DocumentSnapshot`
    - 条件をつける時にはwhereを使う
python

```
In [25]: [d.to_dict()["text"] for d in db.collection("pieces").where("text", "<", "t").stream()]
Out[25]: []

In [26]: [d.to_dict()["text"] for d in db.collection("pieces").where("text", ">", "t").stream()]
Out[26]: ['test']
```

    - [https://googleapis.github.io/google-cloud-python/latest/firestore/client.html](https://googleapis.github.io/google-cloud-python/latest/firestore/client.html)
- Web JS API
    - [Firebase を JavaScript プロジェクトに追加する  |  Firebase](https://firebase.google.com/docs/web/setup)
        - まずscriptタグでいくつかのJSを読み、それから設定する
        - ローカルファイルシステムから開いたのでは動かないJSがあるそうだ
            - firebase-toolsでサーブする
            - Pythonのhttp.serverでも良いと思うがまずは言われた通りにしてみることにした
            - > Error: Cannot understand what targets to deploy. Check that you specified valid targets if you used the --only or --except flag. Otherwise, check your firebase.json to ensure that your project is initialized for the desired features.
            - うーむ
            - `$ python3 -m http.server`
                - で特に問題なさそうだ
            - リリース時には [Firebase Hosting  |  Firebase](https://firebase.google.com/docs/hosting/index) を使うのが手軽そう
    - [Cloud Firestore を使ってみる  |  Firebase](https://firebase.google.com/docs/firestore/quickstart)
        - JSの場合、setやgetはPromiseを返してくる
js

```javascript
db.collection("pieces").get().then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(`${doc.id} => ${doc.data()["text"]}`);
    });
});
```


- REST API
    - [https://firebase.google.com/docs/firestore/reference/rest/v1beta1/projects.databases.documents/createDocument](https://firebase.google.com/docs/firestore/reference/rest/v1beta1/projects.databases.documents/createDocument)
