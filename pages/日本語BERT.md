
日本語で[[BERT]]を使う上で、本家Googleの公開しているモデルは日本語の扱いに問題があるため学習し直したモデルを配布している方がいる。ありがたい。

- [BERT日本語Pretrainedモデル - KUROHASHI-KAWAHARA LAB](http://nlp.ist.i.kyoto-u.ac.jp/index.php?BERT%E6%97%A5%E6%9C%AC%E8%AA%9EPretrained%E3%83%A2%E3%83%87%E3%83%AB)
    - > 入力テキスト: 日本語Wikipedia全て (約1,800万文)
    - > 入力テキストにJuman++ (v2.0.0-rc2)で形態素解析を行い、さらに[[BPE]]を適用しsubwordに分割
    - 論文 [https://www.anlp.jp/proceedings/annual_meeting/2019/pdf_dir/F2-4.pdf](https://www.anlp.jp/proceedings/annual_meeting/2019/pdf_dir/F2-4.pdf)
        - SentencePieceを使わなかった理由:
            - > 形態素解析を行わずに生文に対して sentencepiece などを用いることも考えられるが、構文解析時の解析単位が大きくずれてしまう恐れがある。
    - スライド [https://speakerdeck.com/tomohideshibata/nlp2019-bert-parsing-shibata](https://speakerdeck.com/tomohideshibata/nlp2019-bert-parsing-shibata)

- [BERT with SentencePiece を日本語 Wikipedia で学習してモデルを公開しました – 原理的には可能 – データ分析界隈の人のブログ、もとい雑記帳](https://yoheikikuta.github.io/bert-japanese/)
    - リポジトリ [https://github.com/yoheikikuta/bert-japanese](https://github.com/yoheikikuta/bert-japanese)
    - [[クックパッド+BERT]] と同じ人だと思うけどこちらはWikipediaを元データとして学習している
        - クックパッド社内のデータを使ったものは公開できなかったのだろう
        - [[SentencePiece]]を使う

- [大規模日本語SNSコーパスによる文分散表現モデルの公開 : hottoSNS-BERTの配布 | 株式会社ホットリンク](https://www.hottolink.co.jp/blog/20190311-2)
    - 86M件のTweetを元データにして学習したもの
    - SentencePieceを使う

[[BERT]]
