
[[Scrapboxカスタマイズ]]

- Chrome拡張を作る
- 多くの人が使うための物ではなく、自分一人のニーズを最大限に満たすものを作る
- [/nishio-custom](https://scrapbox.io/nishio-custom)を名前空間代わりに確保した
    - /nishio-custom/sort みたいに使う

- 調査：Chrome拡張はどうやって作るのか
    - [Getting Started Tutorial - Google Chrome](https://developer.chrome.com/extensions/getstarted)
    - とりあえずこれを読めばいいのかな

- 機能

    - [/sushitecture/Scrapbox APIで遊ぶ話](https://scrapbox.io/sushitecture/Scrapbox APIで遊ぶ話)
        - APIの返り値など
        - ページを任意位置配置する
        - [[KJ法]]使いとしては十分な機能があればガチで使いたい
        - 優先度は低い
            - KJ法はScrapboxに限らず汎用的に使えるがScrapbox拡張で実現してもScrapboxにしか使えないから
            - iPadでKJ法できると便利～
                - Scrapboxと独立に
                - 後で別ページにする
        - Chrome拡張で ScrapboxのDOMを抜き取ってKJ法アプリにインポートできると良い
        - 束ねたグループに対してして表札をつけた時に各ヒージが Scrapboxなら末尾にリンク追加してくれるといい

    - ツリーの深いところを非表示にするスライダー
        - [/customize/Hierarchy Extension](https://scrapbox.io/customize/Hierarchy Extension)
        - これ、特に書籍の構成案を練る時に細部を隠して全体を眺められるので便利
        - (本体機能に入って欲しいレベル)

    - include
        - ページ中のincludeリンクを個別or一括でリンク先のコンテンツで置換する
        - 書籍原稿を作る際に、節の単位でページ作って、まとめて章の単位でレビューできる
        - これがないせいで書籍の執筆にScrapboxをガチで使えていない
            - 書籍規模の情報の構造化をしようとしたときに力不足
        - この機能があったら解決するのかどうかは未知数だが実験したい
        - [[Scrapboxで書籍の執筆をしたい]]

- Chrome拡張以外の選択肢
    - Electronでネイティブアプリ化する？
        - 主にローカルファイルシステムを触れることで何か面白いことができないか、という気持ち
        - [Electronでアプリケーションを作ってみよう - Qiita](https://qiita.com/Quramy/items/a4be32769366cfe55778)
            - ローカルアプリパスワードを入れるのが嫌な人もいる
    - PWAは？
        - [いまさら聞けないPWAとAMP - Qiita](https://qiita.com/edwardkenfox/items/4c0b9550ffa48c1f0445)
        - 今回やろうとしている「Scrapboxを機能拡張する」には向かなさそう
