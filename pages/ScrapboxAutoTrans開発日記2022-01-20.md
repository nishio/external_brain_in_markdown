
from [[ScrapboxAutoTrans開発日記2022-01-19]]

from [/villagepump/2022/01/20](https://scrapbox.io/villagepump/2022/01/20)
- [/villagepump/複数言語でScrapboxを運用する](https://scrapbox.io/villagepump/複数言語でScrapboxを運用する)
    - 自分の日本語プロジェクトと英語プロジェクトをどうやって[/villagepump/複数のprojectを透過的に扱う](https://scrapbox.io/villagepump/複数のprojectを透過的に扱う)しようかなと頭を悩ませてたけど、そもそも一つのプロジェクトにしたらいいのかもと思い始めた
        - なぜプロジェクトを分けたのかというと、英語しか読めない人にとって僕の日本語プロジェクトのトップページはゴミの山に見えるから
        - その結果、相互に関係のあるプロジェクトが分断されて「プロジェクト間のつながりを発見する仕組みが必要」と思うようになった
        - 本質的に必要だったのは「英語話者向けコンテンツだけ絞り込んだビュー」だったのでは
            - [/villagepump/Scrapboxは絞り込みが貧弱](https://scrapbox.io/villagepump/Scrapboxは絞り込みが貧弱)だからそれを実現できなかった
                - リンク先の議論を見て「絞り込んだものに対してのビューが貧弱」だったなと気づいた
            - ScrapboxReaderでできるかも？
                - [[アイコン記法で属性表現]]して英語話者向けフラグを立てれば
                - 全部のページに特定のアイコン記法を書いて…めんどくさいな…
                - 自動書き込みすればそこまで面倒でもなさそう<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
    - 開発しつつあるものの根本的存在理由に関わる疑念が発生してしまったとき、どうすればいいのかw
        - ビブラムを履いて散歩するかw
    - 方針定まった
        - [[ScrapboxAutoTransプロジェクトの今後の進め方について方針が決まると良い]]
        - 機械翻訳は一旦ペンディング
        - 二つのプロジェクトをScrapbox上でマージする
            - 英語版のプロジェクトにアイコン記法で英語である旨のフラグを立てる
            - [[intellitech-enのマージ]]
        - ScrapboxReaderで英語話者向けに英語フラグ付きのものだけを表示するビューを作る
