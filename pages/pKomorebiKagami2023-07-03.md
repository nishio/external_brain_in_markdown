---
title: "pKomorebiKagami2023-07-03"
---

[[pKomorebiKagami]]
- [[pOmoikane]]
- [[pPersonalPolis]]と[[pMAGI]]はいったんこれに吸収されそう


from [/omoikane/Polis的システムを作る](https://scrapbox.io/omoikane/Polis的システムを作る)
[[Polis的システム]]
- [[Polis]]に相当する部分の自前実装を作らないと技術的に面白いところがあんまりないなーと[[LLM Meetup TokyoのLT資料を作る]]をやっていて思った<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

泥臭い「土台」の部分を作る<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- [[作成されたショートショートを読んでAIと会話をするツール]]では表面的なUIに着目してた
- が、データを雑にFirestoreに入れると後から苦しくなりそう
- 後々の統計のやりやすさを考えるとやはりRDBでは？
    - [ChatGPT log](https://chat.openai.com/share/275095cc-f389-4d9c-8b24-1e9d13520546)
    - Firestoreに入れると単に数を数えるだけで辛いことになる

ネーミング
- [[コモレビカガミ]]になった

pKomorebiKagami

プロジェクトkomorebi-kagamiを作る
- PostgreSQLインスタンスを作成
    - のためにはCompute Engine APIを有効にする
- うーん、どういう設定でどれくらいの課金になるのか肌感がないぞ
- 何もわからないが開発環境構成で作成した
- 次に何をしたらいいんだろう

テーブル設計
- ユーザ認証はFirebase Authがやるので自前でRDBに待つ必要はない
- 大前提として一つのトピックの中に複数の「はいかいいえで答えられる問い」がある
- 問いの情報もRDBに入れなくて良いのではないか？
    - うーん？どっちかな？
    - 入れなくていい気がするなら性能より柔軟性を重視しよう
        - 後で問題になった時点で入れればいい
- 投票内容についてのテーブルは、トピックのIDと、投票者のIDと、問いのIDと、1,0,-1のいずれかの値を取る投票内容になる、投票時刻も一応つけとこう
- <img src='https://scrapbox.io/api/pages/nishio/GPT/icon' alt='GPT.icon' height="19.5"/>この設計では各ユーザーが各トピックの各問題に対して1回だけ投票できます
    - うーん、そんなことないよな
    - 投票時にすでに投票が存在する時に上書きする設計にするか、常に追加しておいて集計時に最新の情報だけ使うようにするか
    - →前者の方が集計クエリが簡単、しかし履歴は取れない

- インデックスを張ったりする必要があるのでは？
    - →✅

- 投票時にすでに投票が存在する時に上書きする設計と、常に追加しておいて集計時に最新の情報だけ使う設計とで、投票時のSQLと集計時のSQLを作って
- →どっちのケースでもSQLの表現能力に収まるので1クエリで済むが、前者の方が筋が良さそう
    - 投票の変化の履歴は取れなくていいかなと思う



- Cloud Shellで接続
    - Cloud SQL Admin API を Enable する必要がある

はー、できたー
- NextJSのTypeScriptコードからPostgresのテーブルに値を入れるところまでできた
- .env.localからパスワードを読んだ時はダメで、ハードコードしたらできた。パスワードの中の$が悪さしている？
    - パスワード変更したらできた

[ChatGPT log](https://chat.openai.com/share/6e15b62f-55c5-4751-8d33-bfd89aff443c)

