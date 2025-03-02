---
title: "書籍スキャンPDFをScrapboxに置く2019"
---

2019-10-08
[[書籍スキャンPDF]]を[[Scrapbox]]に置く
- [https://www.facebook.com/toshiyukimasui/posts/10157675595687498](https://www.facebook.com/toshiyukimasui/posts/10157675595687498)
    - [Gyazo](https://gyazo.com/api?lang=ja) Gemがある
    - [masui/Book2Scrapbox: 自炊本をScrapboxで読む工夫](https://github.com/masui/Book2Scrapbox)
- 画像にバラした後スクリプトでGyazo Proにアップロード
- Gyazo ProはGoogle Cloud Platformの[[CLOUD VISION]] APIを使って[[OCR]]している
- 時間がかかるのでしばらく経ってからOCRデータを取得している

[https://github.com/masui/Book2Scrapbox](https://github.com/masui/Book2Scrapbox) の読解
- ScanSnapでのスキャン結果を[[pdfimages]]で取り出している
    - 関連 [[PDFからPNGへの変換]]
    - 裁断スキャンPDFならそれでOK
    - スライドのPDFなどはNG
- ローカルにMD5ハッシュでフォルダを切って保存している
- それをAWSにsyncする
    - [AWS コマンドラインインターフェイス（CLI: AWSサービスを管理する統合ツール）| AWS](https://aws.amazon.com/jp/cli/)のインストールが必要
    - [AWS CLI のインストール - AWS Command Line Interface](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-install.html)
        - めっちゃ親切に書いてあるな
    - [AWS CLI の設定 - AWS Command Line Interface](https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/cli-chap-configure.html)
    - [[aws s3 sync]]
        - 手元で削除してもS3上のものは削除されないので安心
- AWSへのsyncは実は必須ではない
    - gyazoにfileの中身を送っているから
- [https://github.com/nishio/Book2Scrapbox](https://github.com/nishio/Book2Scrapbox)
    - スライドはpdfimegesで画像化できないので[[pdftocairo]]を使う
        - `$ pdftocairo -r 200 -f 0 -jpeg <pdf> pages`
            - see [[PDFからPNGへの変換]]
    - 複数のPDFをまとめて1つのJSONにするようにした
    - pdfstojson.rbがmakejson.rbを呼び出す
        - Pythonでやる方法も調べたが、makejson.rbを子プロセスとして使う形で実現できた
    - JSONができてしばらくしてからGyazoからOCR結果をダウンロードして加筆する


[Facebook](https://www.facebook.com/nishiohirokazu/posts/10219634470988868)

