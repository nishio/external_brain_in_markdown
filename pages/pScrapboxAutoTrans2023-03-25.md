
2023-03-25 [[pScrapboxAutoTrans]]

翻訳したものをこのScrapboxに入れるのかどうか
- [[Engineer's way of creating knowledge]]で書籍丸一冊分のコンテンツが英語で入れてあるわけだが、その後1年近く経って、まったく「つながった！」という経験がない
    - たまに予期せずつながることはあるけど、嬉しい繋がり方ではない
- 翻訳したものが即座にこのScrapboxに別ページとして追加されると、似たページが2枚ずつ並ぶことになる
    - イマイチ
- ページに日本語と英語を併記する
    - この方がマシだがイマイチだと思う
- 根本的にはページ一覧がカスタマイズできないことが問題

[[英語発信支援]]
- > Scrapboxに気軽に書いたのを自動的に機械翻訳して英語版のScrapboxプロジェクトに転記した上で英語アカウントでツイートし、リアクションがあった時に僕に通知が来るようにして[[社会的トリガー]]を仕掛けるというのはどうか
    - 英語アカウントでツイートしをしていない
    - Twitter上でのリアクションはない

[[Scrapbox英語化計画]]
- > ScrapboxのAPIでは逐次的アップデートを実現するの面倒そう
    - Yes
- > スモールスタートとして、まずJSONでエクスポートして翻訳してインポートしたらいい
- > 先頭行に`(auto-translated from [Japanese http://....])`と挿入する？
    - 先頭行に機械的テキストを入れるとカード表示が[[ゴミ屋敷]]になる
    - 先頭に入れるならアイコン記法

[[ScrapboxAutoTrans開発日記2021-12-28]]
- > 将来的にはGithub Actionで静的ファイルとして吐いてGithub Pagesとかでホストすると良いのではないか
    - まあ少なくとも僕が死んでnhiroドメインの維持費が支払われなくなって、消滅してから死んだことに気づかれるかもしれないからドメインは分散した方がいいね

2023-03-26
寝て起きる

問題が複雑
- 日々更新されていくドキュメントをどう翻訳するか
- 翻訳されたものをどう見せるか
- 翻訳されたものをどこに置くか
[[シンプルな問題に分割する]]べき

Github Actionで取得するところまではできている
- 翻訳したデータもおけばいい？
- 翻訳するまでもなくすでに英語なものがある？
    - 手動で翻訳したコンテンツがあるよな

- 見積もり
    - 13,115,848文字
- from [[エンジニアの知的生産術英語化プロジェクト]]
    - > 全部エクスポートして見積もって見たら24M文字あるので[[全部翻訳すると6万円]]掛かることがわかった
- from [[機械翻訳の費用]]
    - > ¥2,500 per 1 million characters
- characterがUnicode characterかbytesか
- bytesなら27,493,421
    - こっちが前回の見積もりに近いね
- 見積もり7万円弱
    - 年収の1%未満であり、今後の1年で生産性が1%向上するなら1年でペイする、という気持ち
- 実行
    - 300ページ走らせてみて400円だった
- 全体実行中
- メモ
    - 細かいこと考えて一年近く放置してたが、もう[[先延ばし]]という選択はなしだろ、今日doneにするぞ、[[Done is better than perfect]]、という勢いで実装したんだけど土壇場で色々閃いたので手を動かさずに悩んでた時よりも良くなった
    - ベクトル検索が使えるのでリンクの文字列が完全一致でない問題は気にしない
    - 行単位でキャッシュしてる
        - なのででかいページに1行追加しても1行だけ翻訳
    - 箇条書きなのでインデントを維持して行単位翻訳
        - インデントと本文を分けてから翻訳してる
        - なので同じ内容のインデント違いはキャッシュヒットする
    - ローカルで言語判定かけて日本語でない行は翻訳せずに素通しする
        - これによってソースコードや画像記法などが翻訳対象でなくなる
    - 誤訳を発見した時、キャッシュを修正する手が使える
- ビューのことは何も考えていない
    - 考えてなくもないか
    - Githubにテキスト形式で置いてるぞ

2023-03-30
- 割とエラーでこけてて、リトライ付けてなかったのでまだ終わってない
    - 変なクエリーでリトライし続けて無駄にお金を使うリスクがあったから、大丈夫とわかるまではエラーは目視した上で手動リトライしてた
- [https://github.com/meganii/sandbox-github-actions-scheduler](https://github.com/meganii/sandbox-github-actions-scheduler)
    - を参考にしてる
- [https://github.com/nishio/etude-github-actions](https://github.com/nishio/etude-github-actions)
    - においてる
    - まだGithub Actionでの実行はしてない
- > [@TwitterDev](https://twitter.com/TwitterDev/status/1641222782594990080): Today we are launching our new Twitter API access tiers! We’re excited to share more details about our self-serve access. 🧵
    - いいタイミング！「自分のScrapboxを1日1回英訳した上でGPTに英語で要約ツイートさせる」をやりたいのでやりやすくなった

- langdetectはやめた方が良さそう
    - 短文に対しては誤判定が多くて、確率的挙動をするから「一度英語だと判定したけど、今度は日本語だと判定したから訳しました」的なのが発生してる
        - [https://github.com/nishio/etude-github-actions/commit/e86ca8e8119c492c72c4c1e58982b7830924c85b#diff-7bd0b7387ba890dfb8a3302f1795f74db56eba845bdd467f9c47f04717bab873](https://github.com/nishio/etude-github-actions/commit/e86ca8e8119c492c72c4c1e58982b7830924c85b#diff-7bd0b7387ba890dfb8a3302f1795f74db56eba845bdd467f9c47f04717bab873)
        - こういう感じで「`#天邪鬼 #悪魔の代弁者`って英語だと思う」って言って１行訳し漏らしたりしている
        - Q: 全文入れたら正しく判定するのでは？ A: それはそう、そして日本語の解説がついてるページに置かれた日本語のないソースコードとかも全部翻訳することになるね
    - 日本語領域の文字を一文字でも含んでたら日本語と判定した方がよさげ


[https://www.deepl.com/account/usage](https://www.deepl.com/account/usage)
- ![image](https://gyazo.com/a40aa315dd34aa7c9ada756b0bfb545a/thumb/1000)
- 今これでページ数的には半分くらい行ってるはずなので、意外と安いな？という感じ

2023/4/1
- 無事完了した
- ![image](https://gyazo.com/796feeeb47fc4b9e3ddcbe3627ec60b0/thumb/1000)
- 2.3万円。予想よりかなり安いね
    - バイト数で見積もって7万円のつもりでいたが、どうやらユニコード文字みたいだな
    - 13,115,848文字 / 27,493,421bytes
    - インデントや改行の除去とキャッシュによる重複文字列の除去がきいて13M文字から9.3M文字に減った

まず0を1にして、それから改善する
- 翻訳されたものをどこに置くか
    - →とりあえずGithubにある
        - →翻訳されたものをどう見せるか
            - [https://github.com/nishio/etude-github-actions/blob/main/nishio/pages_en/59280ec2ba093700118f9bc5.json](https://github.com/nishio/etude-github-actions/blob/main/nishio/pages_en/59280ec2ba093700118f9bc5.json)
            - なんで赤いんだろうって思ったけどこれ、拡張子がjsonなのに中身がscrapboxじゃん
            - Markdownに変換することができればGithub上でも読むことができる
            - だけどScrapbox的にリンクが繋がるようにするのは骨だと思うね
            - Githubから[[mem.nhiro.org]]が読み込むことはできるだろうか？
- 日々更新されていくドキュメントをどう翻訳するか
    - Github Actionsで更新できるかトライしよう
    - 手元での時間計測
        - `python main.py  2578.84s user 270.36s system 98% cpu 48:27.16 total`
        - なんでそんなに時間が掛かるんだ？
        - あ、キャッシュの更新か
        - 直した [Github](https://github.com/nishio/etude-github-actions/commit/98ac9d7e2267f3bc7faf2c02720c7d00bb7638b2)
            - `python main.py  3.73s user 2.56s system 68% cpu 9.118 total`

この一週間の間の更新を再クロール
- `python main.py  39.36s user 14.77s system 10% cpu 8:49.13 total`
再翻訳
- `total 28492485 no_cache 156769 ratio 0.005502117488172758`
- `python main.py  48.04s user 7.02s system 3% cpu 24:02.17 total`
    - 翻訳APIの待ち時間がほとんど

Github Actionsで実行
- 1時間経っても終わってない
- どこが遅いのかもっと詳細に調べたいな
- ページの取得と翻訳を一つのスクリプトにしてしまったからどっちが問題なのかとかわからない
    - 取得が遅い場合
        - 全部取ってるからそりゃそうだ
            - 最初に候補を出す段階で更新日時はわかっているので、更新されてるものだけ取れば良い
            - 自分が管理権限を持ってるものに関してはexport APIでもよい
    - 翻訳が遅い場合
        - APIのレスポンスを直列で待ってるからだな

6時間掛かってキャンセルされてる
- ![image](https://gyazo.com/7da36b796fac0b2cdaba26c2e1fe6ff1/thumb/1000)
- ログを見た
- クロールは完了して、翻訳をしてる最中で止まってる
- `  9%|▉         | 1368/14461 [00:00<00:07, 1831.53it/s]`
    - キャッシュが効いてなかったらもっと遅いと思うのだが...
- `Error: The operation was canceled.`

2023/4/5
- キャッシュが効いてない可能性を疑ったがそんなことはなかった
- 状況を確認するためにデバッグ出力をいろいろ変更したのだがなぜかあっさり完了した。は？
    - 一晩寝て気づいたんだが、もしかしてプログレス表示がイレギュラーなターミナル操作をすることと、Github ActionsのログをキャプチャしてWeb上でリアルタイムに見せるための仕組みの相性が悪かったのかも？

2023/4/6
- まずはScrapboxに自動インポートする
    - 理想としては[[mem.nhiro.org]]につなげるのが良いが、まずは手軽な一歩から
- 活動ダイジェストを自動Tweetしたい
    - まずは手軽なところから「Tweet内容をファイルに出力」「人間がそれを見てTweet」

[[実験2023-04-06]]

from [/villagepump/2023/04/07](https://scrapbox.io/villagepump/2023/04/07)
- Scrapbox機械翻訳結果を見て、初っ端から「Yasukazu Nishio」と訳されてるのを見てガッカリしている
- 昼休みにChatGPT Pluginが来てることに気づいた
- 翻訳を改善する話は吹き飛んだ
- ということをあとでメモしておかないと「なんでやめたんだっけ？」になる

next [[pScrapboxAutoTrans2023-04-18]]
