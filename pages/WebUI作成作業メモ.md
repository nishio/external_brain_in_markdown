---
title: "WebUI作成作業メモ"
---

[[pKeicho]]にWebUIをつける作業
- [[WebUI作成作業メモ1日目]]

次にやること
- トークIDが指定されたときに、それをFirebaseから読んでログ表示する
- 会話の表示部分はこのままでよくて、入力欄は隠し、あとメニューから高度なエクスポートのためのダイアログが開く

- ハッシュで渡された会話IDをパースする
    - [URLSearchParams - Web API | MDN](https://developer.mozilla.org/ja/docs/Web/API/URLSearchParams)

- ログを表示するだけならサーバを介さずにFirebaseから直接読めば良い
    - `$ npm install firebase`
    - [[npmの--save]]
    - firebase@8で型エラーになる
        - よくわからない。@7にした

- ログ表示できた
    - [https://keicho.netlify.app/#talk=I9IlVW6Xt58NlNHAjdfq](https://keicho.netlify.app/#talk=I9IlVW6Xt58NlNHAjdfq)
    - メモ: 人間が会話した後、このログ表示用のURLを得る方法がない、後でつける
- 次はRegroup用のエクスポート機能だ

- メニューアイテムと全画面ダイアログで良さそう
    - Material-UIのMenuは最新のReactのStrictModeでは警告が出る
    - [[FIXED:Material-UIでメニューが閉じない]]
    - ![image](https://gyazo.com/1250d54f4717becec7fc6ff53b2f10c6/thumb/1000)
- 次は全画面ダイアログ
    - ![image](https://gyazo.com/164ee185463bfa29adafe6e89306c80e/thumb/1000)
    - ![image](https://gyazo.com/33382aa26072481d3b68a61b2e214982/thumb/1000)
- ![image](https://gyazo.com/e52316181ce2e614ef9a873c48da5cd0/thumb/1000)
- Regroupに貼り付けてから行分割をポチポチクリックしたけど、どうせ全部分割するのだから、エクスポートを押したらサーバサイドで全部分割してRegroupにインポートして開くところまでやってくれたらいい気がした
- 現状のログオブジェクトでは抽出されたキーワードと会話とがバラバラになってしまうが、これはやっぱり時系列に並んでた方が整理しやすい
    - あとユーザの「まず聞いて」コマンドなども拾っちゃうので、エクスポートするときに取り除いてやるのが親切

> メモ: 人間が会話した後、このログ表示用のURLを得る方法がない、後でつける
- 簡単だと気づいたからメニューに追加しておいた

散歩しながら使ってみた
- [[会話ログ20210121]]
- 付箋に刻むと312枚になった、これはちょっと大変だな…
    - ![image](https://gyazo.com/634bfb47b5ea5d820c5e39eca46524b9/thumb/1000)
    - ![image](https://gyazo.com/bebc95b7f324a0b14fbfd9a755a035ac/thumb/1000)
    - あんまり収拾ついてない
    - 根本的に話が複数あるんだな

Scrapbox形式でのエクスポートも実装した
