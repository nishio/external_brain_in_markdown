---
title: 'VSCode: "読み取り専用のエディタは編集できません"の解決法'
---

高校でVisual StudioでC++を学んでいて、復習のために自宅のMacに開発環境を作りたい、という話を聞いた。
[C++の開発環境をVisual Studio Codeのみで構築する | クラインのIT備忘壺](https://klein-itblog.com/mac-cplusplus-development/?fbclid=IwAR29XwpqmTBmCDJXmStbNeo5jCzPlvcxQFj4_9Uki67x2hUwTusB7BKn7Vc)
Visual Studio Codeと、その拡張機能のCode Runnerを使うことで手軽に開発環境を作ることができる。

ところがこれを使って作ったプログラムに入力をしようとすると「読み取り専用のエディタは編集できません」というエラーメッセージが表示される。
これはデフォルトの設定では以下のような仕組みだから。
- プログラムを実行する
- →その結果を読み取り専用で表示する

「入力を受け取るプログラム」を動かすには下記の双方向のやり取りが必要。
- ユーザのキー操作を受け取る→プログラムに入力
- プログラムの出力→画面に表示してユーザに見せる

このユーザのキー操作を受け取ったり画面に表示したりするプログラムを、しばしば「ターミナル」と呼ぶ。

プログラムの中でstdin, stdoutなどの単語を目にすると思う。
- これはstandard input, standard outputの略。
- 日本語でいうと「標準入力」「標準出力」
- 参考: [標準ストリーム - Wikipedia](https://ja.wikipedia.org/wiki/%E6%A8%99%E6%BA%96%E3%82%B9%E3%83%88%E3%83%AA%E3%83%BC%E3%83%A0)

これをターミナルと接続することで、双方向のやり取りができるようになる。
- ターミナルがユーザのキー操作を受け取り、あなたが書いたプログラムのstdinに入力する
- あなたがstdoutに出力したものが、ターミナルに表示される

設定方法はこちら: [Cannot edit in read-only editor VS Code - Stack Overflow](https://stackoverflow.com/questions/54856374/cannot-edit-in-read-only-editor-vs-code?fbclid=IwAR1vkc88bCXyukgOmUVtgOXK2tpNe_L_pWEJLywjdwNfA8z0x-9jvcTzIl8)
