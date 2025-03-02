
本家: [/RealURL](https://scrapbox.io/RealURL)
- リンク先が404 Not Foundの場合に、あらかじめブラウザに登録しておいたパスワードによってURLを変換してリダイレクトするChrome拡張
- つまり、公開の場からリンクを張りつつ、そのリンク先を見ることができる人をパスワードで制限できる
- 例えば、公開のこのScrapboxから、Dropbox上のPDFにリンクを張ると、普通はPDFが誰にでも見えてしまう
    - [https://www.dropbox.com/s/vayss2xht3t5r3h/history_of_com.pdf?dl=0](https://www.dropbox.com/s/vayss2xht3t5r3h/history_of_com.pdf?dl=0)
- このURLを暗号化すると、パスワードを知っている人しかアクセスできなくなる
    - [https://www.dropbox.com/s/vayss2xht3t5r3h/enmrrwa_fy%5Bqzj.pdf?dl=0](https://www.dropbox.com/s/vayss2xht3t5r3h/enmrrwa_fy%5Bqzj.pdf?dl=0)
- パスワードを使ってURLを変換する作業はChrome拡張が自動的に行うので、パスワードを登録した人間にとっては普通のリンクと同じに感じる
- これがとても便利なユースケース
    - DropboxにおいたPDFが、例えば再配布の禁止されている論文や書籍のスキャンの場合
    - その論文や書籍の読書メモを公開の場に書いている場合、そこからPDFへのリンクを張れると便利
    - しかし、今までのリンクではリンク先が公開されてしまうためできなかった
    - この拡張によってURL自体を暗号化すれば、公開の場にリンクを置き、かつ自分しかアクセスできない
    - [[プライベートリンク]]と同じ使い方ができる
