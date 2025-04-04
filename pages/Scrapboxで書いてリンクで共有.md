---
title: "Scrapboxで書いてリンクで共有"
---

- 旧タイトル「ScrapboxとGoogleDocs」
    - チャットで盛り上がった話を「これは有益だからまとめとこう」と思った
        - Scrapboxでまとめた
        - それをチャットに参加してた人に共有しようと思ったときにScrapboxでは「リンクで共有」ができない。
    - 公開できない話なので僕のpublicに置くわけにもいかない。
    - 新しいprivateプロジェクトを作ったとしても…
        - インバイトリンクは個別のページに貼れない
        - 「このリンクからグループに入って、それからこのページを見て」と二度手間
    - 「リンクを1個貼って『ここにまとめときました』と言いたい」というユースケース
    - 僕はいままとめてるやつをあとでGoogle Docsに移植して「[[リンクで共有]]」することになるのだろうか面倒

- 一晩寝て起きたら解決策を思いついた
    - Scrapboxでまとめた後、ブックマークレットでMarkdownに変換
        - [Scrapboxページの文章をMarkdownに変換するBookmarkletを書いた](http://daiiz.hatenablog.com/entry/2017/02/17/074508)を使う
    - そのMarkdownを[HackMD - 共同編集できるMarkdownノート](https://hackmd.io/)に貼ればよい
        - リンクを知っている人だけが[[共同編集]]できる
    - ただし上記ブックマークレットは現時点ではネストした箇条書きが正しく変換できない。
        - 変換後の出力を`s/^( +)/\1\1/`したらOK
            - 作者にフィードバック済み
    - 将来的にはMarkdown書き出しが公式にサポートされるといい

- ページ間リンクが強みのScrapboxなので、1ページ共有するって目的だと正直他のサービスと大差ない
    - 逆に言えばScrapboxで書いて問題ない、ストレスなく1ページMarkdownでエクスポートできたらいいだけ
    - 箇条書きの整理に関するショートカットが充実しているのが長所？
        - [/help/アウトライン編集](https://scrapbox.io/help/アウトライン編集)

- GoogleDocsは今回は使わない結論になったが「コメント」「編集差分」の機能が充実しているのが長所
    - だけど「チャットでの議論をざっくりまとめときました～」的ユースケースでは編集差分のハイライト表示はいらんわな
    - コメントつける機能はDropboxなら箇条書きをツリー掲示板的に使う形の文化が出来つつあるみたい
        - 本文とコメントが分離していないという問題点はある
    - Web記事の添削とかには便利

- [Dropbox Paper](https://www.dropbox.com/paper)も仕事の一つで使っている
    - 他の3つの方法と比べた時の大きな違いは…
        - デフォルトでタスクトレイに入っているDropboxアイコンで更新通知をしてくるぐらいか？
    - [[更新されたことをどう通知するか]]、というのはユーザーに使い続けさせるために重要な要素
        - またの機会に。

- HackMDで共有した後にそれを編集した場合、どうやってScrapboxに戻すのかという別の問題が。
    - HackMD上だけで編集してたならScrapboxに変換しなおして上書きすればよいが
    - Scrapboxでも編集していた場合はどうやってマージするんだ問題が発生する
    - 両方Markdownにしてマージ？