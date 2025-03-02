
prev [[ScrapboxAutoTrans開発日記2022-01-13]]

インクリメンタル静的再生成
- ![image](https://gyazo.com/6dc186055d1a7478fdc2b3d4322fe330/thumb/1000)
    - [https://vercel.com/docs/concepts/next.js/incremental-static-regeneration](https://vercel.com/docs/concepts/next.js/incremental-static-regeneration)
- 開発過程の試行錯誤はすぐ反映されて欲しいけど、安定運用に入ったら60×60×24でもいいかも
- どちらにせよ翻訳のサイクルは別だよなぁ感
- 2ホップリンクがバグってたのを直した
- Google Analyticsを入れようとして生のHTMLを書けないことに気づいた
- リンク先のJSONがあらかじめfetchされてるのか！
    - ![image](https://gyazo.com/d06ac322e1ff1e63372dae3704d6568b/thumb/1000)
- mem.nhiro.orgとかにマップしようかな
    - memo, memory, memex, mememt moriなどの匂わせ
- 翻訳も目指してるけど、先に一覧ページが必要かなー
    - [[Scrapbox振り返り機能]]
    - これ、ページが作られるのがウザくて結局使ってないのだが、固定URLを開けばこの振り返りリストが出る仕組みならいいのでは、と思っている
        - `https://scrapbox.io/api/pages/nishio/search/titles?followingId=5a893319c2a2f300142bde60`
- 管理者メニュー
    - ユーザが僕であることを認識してこれとかのメニューを出す
        - [/porterapp/SafariのScrapboxのページからPorterへスイッチ(Switch from Safari to Porter)](https://scrapbox.io/porterapp/SafariのScrapboxのページからPorterへスイッチ(Switch from Safari to Porter))
- 翻訳
    - タイトルの翻訳後の英語文字列をキーとして翻訳語のtextが得られる必要がある
    - 翻訳日時を記録する
        - 前の翻訳から変更されてなければ再翻訳の必要はない
    - 翻訳のトリガーはアクセスでなくて良いと思う
        - まず一括で翻訳する必要がある、タイトルが確定しなければアクセスされもしない
        - その後は1日1回、過去24時間に更新されたものを再翻訳
        - はてなダイアリーの流し込みみたいに古い日時でながしこんだものは翻訳もされない流し込んだものは翻訳されないがどうするか？
            - 上記の「過去24時間に更新されたものを再翻訳」する際に、そこからリンクされてるものが翻訳済みか確認する？

2022-01-18
[https://nextjs.org/docs/api-reference/next/link](https://nextjs.org/docs/api-reference/next/link)
