
- 自作電子的KJ法ツール改善プロジェクト
    - 5年くらい前に作って放置していた[[自作電子的KJ法ツールgrouping]]
    - iPad Pro + Apple Pencilを前提としたら割と良いのではないかと思ったので再始動([[2018]]-09-19)
    - 開発コードネーム [[Regroup]]

[[iPadでの開発]]

- 編集はPencilを使うことにする
- SVGでの重なり順序の問題
- データをCloud Firestoreに保存する

-----
- 移植のために以前のバージョンで使った[Google Realtime API](https://developers.google.com/realtime/overview)を確認したら来年1月に終わるって書いてあった
- [データベースを選択: Cloud Firestore または Realtime Database  |  Firebase](https://firebase.google.com/docs/database/rtdb-vs-firestore?hl=ja)
- [Cloud Firestore データモデル  |  Firebase](https://firebase.google.com/docs/firestore/data-model?hl=ja)

- 過去のバージョンのデータ構造: `[{text, when, id, x, y}]`
    - グループ化とか矢印とかは保存機能を未実装だった
    - 作業プロセスを後で見ることができると面白いのでhistoryって形で[[変更履歴を保存]]しても良さそう

- [中〜大規模なSPAを開発する時に抑えておきたい10のポイント - KAYAC engineers' blog](https://techblog.kayac.com/10-spa-knowhow)
    - クライアントサイドルーティングとは何か？
        - [SPAのルーティングの話](https://www.slideshare.net/ushiboy/spa-76170499)
        - 昔Hashでやってたようなことが高度化してるみたい
    - [フロントエンド開発に Babel も Webpack も必要ない ※ - KAYAC engineers' blog](https://techblog.kayac.com/pure-js-app)
        - importできる
            - [import - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/import)

- [オフライン データを有効にする  |  Firebase](https://firebase.google.com/docs/firestore/manage-data/enable-offline?hl=ja)
    - あとで。

- [[Firestore]]
-----
React版ではiPadで表示した際にテキストタッチでテキストが消える現象は発生しないので、古いバージョンのRaphaelの問題だろう

-----
- iPad Proで自分が使うことを想定して新バージョンを作る
    - UIをiPadむけにする
    - [[初期状態でズームアウトした全体表示モード]]
- 設計指針
    - ズームアウトした表示の時に意味がある表示でなければならない [[ズームアウトした時に意味のある表示にする]]
        - 「付箋がどっさりあってすごいね」だけしかわからない表示は意味がない
        - フォントサイズの下限を決めて、それより小さい文字は人間が視認できないと判断して非表示
        - それによってできる広い表示空間を使って、表札などの高度な付箋タイトルを拡大表示
            - イメージとしてはシムシティなどにおいて全体マップを表示した時に地名などが表示されるもの
    - [[ズームインした表示の時に画面外にものがあることに気づけなければならない]]
    - グループは明示的に作らなくてよいのではないか
        - 明示的なグループの所属関係があると、入れる、出す、が必要になる
        - まとめて移動する時、畳む際に初めて、どれが畳む対象か指定すればよい
        - まとめて移動する対象が必ずしもグループとは限らない
- [http://nishio.github.io/idea-generation/grouping/#fileIds=1cED4uxHbS3ylaD13-X3sNnyV4dDbnq83&userId=112643481944466832095](http://nishio.github.io/idea-generation/grouping/#fileIds=1cED4uxHbS3ylaD13-X3sNnyV4dDbnq83&userId=112643481944466832095)

-----
- 作成当時は画面が狭すぎて実用的ではなかった
- iPad Proで開いて動作確認した。
    - 開いてすぐズームアウトは受け付けない(タブ表示に遷移しちゃう)
    - ズームインした状態ならズームアウトできる。
    - 2本指ジェスチャでズームイン、平行移動ができる。
        - →開いた時点で付箋全体が見えるところまでズームアウトしておき、そこからズームインして使えばよいのか？
    - 付箋の移動は指でもPencilでもできる
        - ただしテキスト部分をドラッグするとテキストが消える謎の現象が起きる
    - デフォルトでは100枚をぴっちり並べて画面いっぱい
        - だけど縦横2倍にしても結構な字数までは読める
        - スムーズで直感的なズームインズームアウトができるなら十分行けるのではないか

- 余計な機能
    - 今のバージョンでは箱と箱に間に[[矢印を書く機能]]などがある
        - 電子的にKJ法をやる上で本当に必要なのは「グループ編成」の支援
        - 矢印加筆などは、グループ編成した後のA型図解化の工程でやること
        - グループ編成のフェーズに矢印機能は必要ない、メニューがたくさんあることによる混乱が有害
        - PCで開発する用のデバッグUIが下にごちゃごちゃとついている
            - iPadで開くとデフォルトで見えてしまう
            - 最初はこれは隠して、開発メニューを押すと出てくるとかがよい
        - 図解化は、スクリーンショット or 画像を書きだしてiPad自体の機能で書きこんだらいい
            - PDF書き出しがあるとよい？

- 足りてない機能
    - 画像を付箋にする
        - 付箋の内容がhttpで始まる場合に画像だと解釈するアプローチでよいのでは
    - グループ化
        - 「束ねるモード開始ボタン→対象付箋をタップ(トグル)→完了ボタン/キャンセルボタン」でよい。
        - 投げ縄ツールを作ったところで「投げ縄モード」「選択」「グループ化」と手数が同じだから。
        - 手順
            - 束ねるモード開始
            - 対象付箋をタップ
            - 完了ボタン
            - 表札を選択or新規作成
