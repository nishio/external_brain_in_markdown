
from [[はてなダイアリーを過去の日付でScrapboxにインポート]]
過去のブログ記事をScrapboxにインポートして半年、とても良い
2021-05-04 [[はてなダイアリー]]を過去の日付でScrapboxにインポートした [script](https://github.com/nishio/scbot/blob/main/from_hatena.py)
2021-12-20
Q: 半年経つけどどう？
- A: すごく良い
    - 自動ブラケティングはしてないのでリンクの体験を壊すことはなく、検索にはきちんとヒットする
    - 「機械的に投稿してはいけない」はもっと解像度高く観察すべきだった
        - 「最近更新したページ一覧」が「人間の活動一覧」から「機械の活動も含めた一覧」になると人間の活動を見る邪魔になる
        - ブラケティングを自動で作ると[[大きすぎるリンクの問題]]が起こりリンクの価値が落ちる
    - リンクを付けずに古い記事を古い更新日時で流し込むことは実害がない
        - たぶん「Tweetを投稿から1ヶ月後に自動でインポート」とかも実害ないと思う
    - 客観的データ
        - [https://scrapbox.io/nishio/search/page?q=%5BHatena](https://scrapbox.io/nishio/search/page?q=%5BHatena)
            - 半年で13のページから過去のブログ記事への言及が発生している
        - [https://scrapbox.io/nishio/search/page?q=d.hatena.ne.jp%2Fnishiohirokazu](https://scrapbox.io/nishio/search/page?q=d.hatena.ne.jp%2Fnishiohirokazu)
            - 2017年4月からの4年間の利用で41ページから元のブログへの言及がある
        - 過去記事とのリンクがおよそ2.5倍に増えた
