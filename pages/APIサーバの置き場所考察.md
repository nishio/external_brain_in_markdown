
どうするのが適切か
- Heroku
    - 使用頻度が低い場合、無料プランでいける
        - 月に1000時間
        - 30分使わないとスリープする
    - 月額$7で常時稼働になる
    - 今は大体これでやってる
    - スリープからの復帰時間が問題になるかも
    - ファイルサイズが大きいと無料の範囲で収まらなくなるかも
        - > Herokuの無料枠のストレージサイズが500MB
            - [Herokuでpython+mecab+ffmpegを使う - Qiita](https://qiita.com/Sashimimochi/items/2da79bda71dfc1b555cd)
    - ワイルドカード証明書でHTTPS化される
- AWS Lambda
    - 選択肢の一つだとは思ってるけどまだ試してない
    - > MeCab はコードにネイティブバイナリを使用しているため、Python のディプロイパッケージを作成する場合は、以下のリンク先で公開されている Amazon Linux AMI を使用して、Lambda 実行環境と同等の環境を構築してそのOS上で、パッケージを作成してください。
        - [AWS Lambda で MeCab を動かす | Developers.IO](https://dev.classmethod.jp/articles/aws-lambda-with-mecab/)
        - [【改】AWS Lambda で MeCab を動かす | Developers.IO](https://dev.classmethod.jp/articles/improved-aws-lambda-with-mecab/)
- Netlify Function
    - Pythonが使えないので自然言語処理するのには向いてない
    - HTML+JSなUI部分の静的配信にはNetlifyを使ってることが多いので、一本化できるならそのほうが良いのだけど。
- AWS EC2

