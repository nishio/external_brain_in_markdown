
Scrapboxにインポートする際、上書きしてコンテンツを喪失したくなければ、まずエクスポートしてローカルでマージしてからインポートするしかない

2019-10-31の調査
- エクスポート
    - `https://scrapbox.io/api/page-data/export/PROJECT_NAME.json` にPOST
        - リクエスト
            - connect.sid積んでる
                - see [[ScrapboxのprivateプロジェクトのAPIを叩く]]
                - ペイロード `{"metadata":false}`
                    - trueにしたら行毎の更新日時とかのあるやつになるのだろう
            - リクエストヘッダにX-CSRF-TOKENが付いているが、これも何らかの方法で取得して積む必要があるかな？？
            - 両方必要っぽい
            - `curl -X POST https://scrapbox.io/api/page-data/export/PROJECT_NAME.json -b connect.sid=SECRET_ID -H "X-CSRF-TOKEN: ..." -o export.json`
                - これでダウンロードできた
        - レスポンス
            - UI的には「ダウンロード」ボタンができてそれをクリックする仕組み
                - てっきりサーバ側でファイルを生成してて、そのリンクになるのかと思ってた
                - しかしレスポンスでプロジェクト全体のJSONが返ってきている
            - ボタンは`<a href="blob:https://scrapbox.io/446e...." download="nishio.json" ...>Click to download...</a>`
            - Blobを作ってそれをファイルとしてダウンロードさせているのだろう
                - `URL.createObjectURL(new Blob(...))`って感じで
                - [Blob - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/Blob)

- マージ
    - あとで

- インポート
    - ページの削除が発生する場合、一旦プロジェクトを削除しなければいけない
        - これは保留
    - インポート対象のファイルを指定した時に、何ページインポートされるかが表示される
        - てっきりサーバに送ってるのかと思ったが、リクエストが飛んでいない
        - クライアントでJSでチェックしているんだな
    - `POST https://scrapbox.io/api/page-data/import/PROJECT_NAME.json`
    - これもconnect.sidとX-CSRF-TOKENを積んでいる
    - Form Dataとしてjsonの中身を送ってるだけに見える
        - name: undefinedだけど、これは特に指定しなくても使わないから関係ないということだろうか
        - `-F "jsonfile=@path/to/jsonfile.json"` でできるかな
