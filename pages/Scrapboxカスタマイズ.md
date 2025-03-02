
- 1年ちょい「生のScrapbox」を使ってきた
- そろそろ機能の不満点を実装でカバーし始めてもよいころ
    - 守破離の守は終わってよかろうという意味

- ここは「こんな機能があったらよいかも」を思いついたときに書くところ

- あいふぉんでの不便は [/porterapp](https://scrapbox.io/porterapp) でかなり解決しそう

- 特定の条件を満たしたページを一覧、一括削除
    - タイトルがSRSで始まるページが生成されたページだけか確認したい
    - そして削除したい

- ページに追記するAPI
    - あるとうれしいのだが、なさそう
    - ブラウザ自動化しかないか？
        - ブラウザ操作自動化で無理やり作ればいいのではないか
        - 他のユーザに提供するのは認証情報の扱いがめんどくさいが自分専用で

- ショートカットキーの追加
    - JSのコマンド [/nekobatoken/Ctrl-cで独自のチェックマークを挿入するUserScript](https://scrapbox.io/nekobatoken/Ctrl-cで独自のチェックマークを挿入するUserScript)
    - [[リンク化]]にショートカットキーをつけたい
    - [/customize/Scrapbox Dynamic Macro](https://scrapbox.io/customize/Scrapbox Dynamic Macro) かなりいろいろやってる例

- JSからの本文へのインサート
    - JSのコマンド [/nekobatoken/Ctrl-cで独自のチェックマークを挿入するUserScript](https://scrapbox.io/nekobatoken/Ctrl-cで独自のチェックマークを挿入するUserScript)
    - [[document.execCommand]]はScrapboxの特殊な機能ではなく、最近のブラウザに生えてるメソッドらしい

- Wikipediaのリンクを貼ったときにタイトルをリンクしたい
    - より一般的には外部リンクを貼ったときにそのページのタイトルでの外部リンクと、タイトルに含まれる文言はキーワードである可能性が高いことから内部リンクとが両方入って欲しい。
    - 今使っているブックマークレットだとこうなる
        - `[Spaced repetition - Wikipedia https://en.wikipedia.org/wiki/Spaced_repetition]`
        - 生URLよりはだいぶマシ
    - 理想
        - `[Spaced repetition]([Wikipedia https://en.wikipedia.org/wiki/Spaced_repetition])`
        - 今から張るリンクがそうなるだけではなく、後から「あー、こういうフォーマットにしとけばよかったなー」って思ったらこびとさんが変更して回ってくれるとうれしい
        - ページサイドのコマンドでページ内を整形するのでもよいかも？
            - でも複数ページを一括して編集する機能は将来的には色々便利

- Amazonへのリンクがもっと手軽にできて欲しい
    - Amazonの商品ページでワンクリックでScrapboxにページが出来ると良い

- 通知フィルタ
    - Slackに通知を飛ばした時に、自分の更新も他人の更新も一緒くたで困る
        - 自分の更新は通知されなくてよいい、他人のは通知されて欲しい
        - Slackの手前に通知を受け取ってフィルタしてSlackに投げるサーバを置く

- JSONの自動バックアップ
    - 標準機能で入ったらしい

- iPadでもアウトライン編集したい
    - 右に隙間があるからここにボタンをフロートさせたい

- 複数のページに「前後」リンクをつけたい

- [[Scrapboxにコメント機能を付ける案]]

- タブとスペースの統一
    - Scrapbox上でJavaScriptのコードを書いていてタブとスペースが混在していて割と嫌

- 入力や更新があった日をGithubの芝みたいに表示

- [[抜き書きUserScript]]
    - カットしないバージョン

- 調査：Scrapboxの使えるAPIは何があるか
    - [/help-jp/API](https://scrapbox.io/help-jp/API)
