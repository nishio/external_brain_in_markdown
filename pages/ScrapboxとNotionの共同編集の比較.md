---
title: "ScrapboxとNotionの共同編集の比較"
---

Scrapboxは何年も共同編集を経験していて、最近Notionでの共同編集を経験したので感じたことをメモしていく。Scrapboxに比べてNotionは詳しくないので「〜に相当する機能がない」は「僕は知らない、あったら教えて」という意味。

Notionはフォーマットが決まっているものを多人数で収集するのに便利。
- [Social Hack Day #50](https://www.notion.so/code4japan-community/Social-Hack-Day-50-84fd842a943c4ab4800011298cc41f55?pvs=4#67339895a76e4e76b546365380493426)
    - ![image](https://gyazo.com/b3177063df3798512bb6329f861ed91a/thumb/1000)
        - TwitterやGithubのIDはルックアップで個人のレコードから取ってきている
    - ![image](https://gyazo.com/ffd083b0cecbd1616296a0ab49518dd5/thumb/1000)
        - 一つ目のフィールドがプロフィールのレコードである、というプログラマの言葉で言うなら「型」があるため、それを使って入力補助をすることができる
        - このフィールドの情報を使ってTwitterなどの情報をルックアップしているのだろう
    - ![image](https://gyazo.com/b70af155c20bf86cf1fd11a3afc829a8/thumb/1000)
        - このページに書かれていることがレコードとして扱われてる
        - なお名前のリンクをクリックしただけでページ遷移することなく右からリンク先のページがにゅっと出てくる
            - この機能、Scrapboxにも欲しい！

Scrapboxと違ってテロメアがないので他の人が画面外を編集している時に気づけない

Scrapboxは目立つところに検索バーがあって、検索しやすくすることにフォーカスしている感じがある
- Notionの検索はここ
    - ![image](https://gyazo.com/8fdffb90c43b6de631d6aa892e62deb9/thumb/1000)

Scrapboxは箇条書きなのでどこにでも行を挿入してコメントをつけられる
- ![image](https://gyazo.com/12acfabff2641dc1670d26619ecd1c3a/thumb/1000)
- Notionは文字列を選択してコメントをつけられる
    - ![image](https://gyazo.com/0474c3c39366ca40e1d00613523a6e97/thumb/1000)
        - [Hackdays定例](https://www.notion.so/code4japan-community/Hackdays-ba72b54a61424ded8f5367d7ef4b3c54?pvs=4#2e12457d83b74633a1a2a36f862c4972)
- 文化によって賛否が分かれるところだ
    - Notionのサイドにコメントとしてつくスタイルは主客が分離する
        - その方が安心という人もいるだろう(本文を汚すのは忍びない、とか)
    - Scrapboxの「どこにでも行を挿入するスタイル」は自分が書いた塊の途中に他の人が挿入した文章によって全体が読みにくくなってしまうこともある
        - 「文章ブロックに対する独占権を認めない」的なカルチャー
            - 読みにくくなったと思うなら読みにくくなったと思う人が清書すれば良いのであって、どこにでも書き込める自由を制限するのは良くない、的なカルチャー
            - コミュニティのメンバーが本気で互いのことを対等だと思ってる必要があるのでは
                - さもないと…
                - 「偉い人」が書き込んできた人に対して怒ったり
                - 「新参者と思ってる人」が書き込むことをためらったり

Scrapboxのページは、それぞれ個別のページ
- Notionの「ページのように見えるもの」はテーブルのレコードだったりする
- ![image](https://gyazo.com/453b174d01a45c080ca1441b7754bd67/thumb/1000)
    - 個別のイベントに関するページがこの中にあるかな？と思うけどこれはイベントのテーブル
        - ![image](https://gyazo.com/17aff6b6c8833276e85d38f7541d31e3/thumb/1000)
    - 実際はこちらにある
        - ![image](https://gyazo.com/0d2bd9a6c64a20afc7bc1d3507d7e7f4/thumb/1000)
    - データ構造の入れ子構造と、人間の考える情報の構造が一致しない


Notionの編集者のカーソルは行単位で出る
- Scrapboxは文字単位

