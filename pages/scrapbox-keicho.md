
Scrapbox上で動く[[聞き出しチャットシステム]]、[/takker](https://scrapbox.io/takker)作。
特に支障なく使える。凄い。

2021-06-28 [/takker/選択範囲をKeichoに尋ねるPopupMenu](https://scrapbox.io/takker/選択範囲をKeichoに尋ねるPopupMenu)
2021-06-30 [/blu3mo-public/ScrapboxでKeichoを使う拡張](https://scrapbox.io/blu3mo-public/ScrapboxでKeichoを使う拡張)
- [[ScrapboxでKeichoを使う拡張]]
2021-07-29 [[選択範囲をKeichoに尋ねるPopupMenu]]
- [[ScrapboxでCtrl+EnterしてKeichoに質問させる]]
- [/takker/scrapbox-keicho](https://scrapbox.io/takker/scrapbox-keicho)
- > ホットキー&複数行&フィードバックボタンに対応させたものが出来ました<img src='https://scrapbox.io/api/pages/nishio/takker/icon' alt='takker.icon' height="19.5"/>
    - [/villagepump/Scrapbox上でKeichoを動かす#6103a646aff09e0000ddb533](https://scrapbox.io/villagepump/Scrapbox上でKeichoを動かす#6103a646aff09e0000ddb533)
2021-07-30
- [/villagepump/今日何をしたらいいかKeichoと話し合う(original)](https://scrapbox.io/villagepump/今日何をしたらいいかKeichoと話し合う(original))
- [/villagepump/scrapbox-keichoの面白い理由を言語化できるといい](https://scrapbox.io/villagepump/scrapbox-keichoの面白い理由を言語化できるといい)
    - copy [[scrapbox-keichoの面白い理由を言語化できるといい]]
    - > <img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='/nishio/nisbot.icon' height="19.5"/>その「新しいエクスペリエンス」は、どんな「新しいエクスペリエンス」ですか？
    - >  それが知りたいんだけど、とりあえずここまでの話で分かったのは「人間が複数」ってところが変わったところだからこういう使い方ではなく他人のログに絡んでいくのが良いのかもな、試してみる！
- [/villagepump/今日何をしたらいいかKeichoと話し合う (乱入)](https://scrapbox.io/villagepump/今日何をしたらいいかKeichoと話し合う (乱入))

Keichoへの流し込み
Keichoは通常モードでは目的の質問からスタートするけども、Scrapbox上で動かすUIができたことでそうでない始まり方を体験できた
- [/villagepump/今日何をしたらいいかKeichoと話し合う (乱入)#6103b420aff09e0000e087c3](https://scrapbox.io/villagepump/今日何をしたらいいかKeichoと話し合う (乱入)#6103b420aff09e0000e087c3)
- 正直、もっと「会話にならないカオス」になると思ってたが、意外とそうならなかった
    - ので流し込みがやりやすくなるようなAPIをつけたらどうかと考えた
        - が、一括で流し込む(そしてレスポンスを長い時間待つ)より、相槌モードを使って流し込んだ方が、流し込み側で進捗のフィードバックができて良い気がした
- 「意外と会話になる」は会話が少なすぎただけではないか、と思って続行してみた
- [/villagepump/今日何をしたらいいかKeichoと話し合う (乱入)#61056b8baff09e000021f53c](https://scrapbox.io/villagepump/今日何をしたらいいかKeichoと話し合う (乱入)#61056b8baff09e000021f53c)
- 考察
    - Aが会話した後Bが会話に参加した場合、現状のボットは人間を区別していないので、Aが既に掘り下げたキーワードについて、Bに「当然このキーワードに関しては熟考済みだよな」という態度で質問してくる
    - Bは実際には(過去ログを読んで分かったつもりにはなっているが)そのキーワードに関しては熟考してないので質問にうまく答えられない
- 質問されて答えることによって思考の表面に具体的な形で浮かび上がることが大事なのかもしれない

[/villagepump/Scrapbox上でKeichoを動かす#6103a646aff09e0000ddb537](https://scrapbox.io/villagepump/Scrapbox上でKeichoを動かす#6103a646aff09e0000ddb537)
- 過去ログを貼ったScrapbox上から会話をするのはScrapbox上にあるのと同等の記憶をKeicho側も持ってるのでいいんだけど、普通にScrapbox側で書かれたページだとKeichoの側は記憶がないからどうなのか
    - ユースケースは両方ありそう
        - Scrapboxで文章を書いていて、今書いている行で詰まったので今書いている行に質問をして欲しい
        - Scrapboxで文章を書いていて、一通り書き終わったが改善したいので好きな場所に質問をして欲しい
            - これに関しては「まず聞いて」モードでScrapboxのコンテンツを全部流し込んでからスタートするという手が考えられる
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この件に関しては、範囲選択して開始することでどの範囲をボットに知っていて欲しいと考えてるのか自然に表現できると思った
        - ただ、選択範囲を一つの発言とするまずい
            - 引用が発言単位なので、1ページある発言をしたら毎回1ページの引用をつけてくることになる
        - なので初回にある程度大きな範囲が選択されてるなら「相槌モードにして一行ずつの発言とする」って処理が必要そう
        - 逆に言えばそれができると過去のどんなページでもいきなり全選択からのKeicho起動で「一番気になる行を引用して質問」ってなると思う

