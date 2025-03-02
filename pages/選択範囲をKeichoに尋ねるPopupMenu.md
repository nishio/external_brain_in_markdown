---
title: "選択範囲をKeichoに尋ねるPopupMenu"
---

[[ScrapboxでKeichoを使う拡張]]
[/takker/選択範囲をKeichoに尋ねるPopupMenu](https://scrapbox.io/takker/選択範囲をKeichoに尋ねるPopupMenu)
- を試してみた

2021-07-29時点のバージョンをコピペして動かしてみる
js

```javascript
import {insertText} from '../scrapbox-insert-text-2/script.js';
```

`https://scrapbox.io/api/code/nishio/scrapbox-insert-text-2/script.js net::ERR_ABORTED 404 (Not Found)`
そりゃそうだ、絶対パスに修正

`Uncaught (in promise) ReferenceError: getTalkId is not defined`
スクリプト二つあるのを見落としてた

`Uncaught (in promise) SyntaxError: Unexpected token ')'`
[/takker/scrapboxのページ中の同名のcode blockを結合して取り出](https://scrapbox.io/takker/scrapboxのページ中の同名のcode blockを結合して取り出)
からコピペして修正

`Uncaught (in promise) ReferenceError: askKeicho is not defined`
[[TamperMonkey]]に下記にあるUserScriptを入れる
- [/takker/askKeicho](https://scrapbox.io/takker/askKeicho)

テスト
keicho.json

```json
{"talk": "Cl72730A3VXGskCtZ6gL"}
```

<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「テスト」は、どんな「テスト」ですか？
おっ、Scrapbox上でKeichoと話せるようになった
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「Keicho」は、どんな「Keicho」ですか？

[/takker/KeichoとのチャットするUserScript](https://scrapbox.io/takker/KeichoとのチャットするUserScript)でも既に書かれてるが「選択範囲を決めることなく、回答を送信したい/ボタン一つやキー一発で送信したい」
- 選択しなくてもページ全体のコンテンツにアクセスすることはできてる
- `[nisbot.icon]`とは別に`[ask_keicho.icon]`みたいなものを作って、ホットキーでそのアイコンより手前の空行でない行を入力とし、アイコンの手前に回答を挿入したらどうか
1

```
テスト(カーソル)[ask_keicho.icon]
```

2

```
テスト
[nisbot.icon]その「テスト」は、どんな「テスト」ですか？
(カーソル)[ask_keicho.icon]
```

2

```
テスト
[nisbot.icon]その「テスト」は、どんな「テスト」ですか？
次の文章(カーソル)[ask_keicho.icon]
```


- むしろこれなら「カーソルのある行」でいいのか？
    - ホットキーが「質問してくれ改行」になるイメージ
- いまKeichoは人間に見せるチャット的UIと密結合に「直前以外の文章に質問するときだけ引用をつける」って振る舞いをしてるけど、常に入力文をレスポンスに含めるようにしてもいい
    - そうするとUserScriptの側はそれを見て挿入位置を決めれる…のかな？
        - Scrapboxに非同期で文字を入れてる仕組みをまだ理解してないや
    - あー、カーソル位置にtextareaが挿入されてるのを使ってるのか、じゃあユーザのカーソル位置にしか書き込めないなぁ
    - これは任意の場所にプログラムが書き込むAPIを用意しないScrapboxの思想があるから難しそう、ユーザが自分で移動するしかないか

- カーソルのある行
    - うわ、Textareaってposition: absoluteで浮かべてるのか
    - XPath
        - `$x("//span[@class='text' and contains(.,'[ask_keicho.icon]')]").slice(-1)[0].innerText`
        - `"\t\n [nisbot.icon] とは別に [ask_keicho.icon] みたいなものを作って、ホットキーでそのアイコンより手前の空行でない行を入力とし、アイコンの手前に回答を挿入したらどうか"`
    - [https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate](https://developer.mozilla.org/en-US/docs/Web/API/Document/evaluate)
    - `document.evaluate("//span[@class='text' and contains(.,'[ask_keicho.icon]')]", document).iterateNext().innerText`
アイコンだからこれで取れるのでは？→誤り
- `document.querySelector("span.text img[alt='ask_keicho']").parentElement.parentElement.parentElement.parentElement.innerText`
- 誤り: カーソルがアイコンの手前にあるときその行は編集モードになってるのでテキストになってる
- ctrl+Enterで起動
    - ![image](https://gyazo.com/ef790c7995282a347141378543f0201d/thumb/1000)
    - おっと…
    - 角括弧で囲われてるとき、それを明示されたキーワードと解釈するKeichoの仕様
    - じゃあ`(keicho)`でいいか

できた
- [[ScrapboxでCtrl+EnterしてKeichoに質問させる]]

