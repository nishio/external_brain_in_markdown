

2023-11-04 井戸端の日記でWikiを作る理由が語られていたのをみて、自分がWikiを作るならその理由は何なのかを書いた
from [/villagepump/自分がWikiを作る理由](https://scrapbox.io/villagepump/自分がWikiを作る理由)
- Keichobot、Kozanebaと密に連携したい
    - 正直作りたいわけではないのでScrapboxに連携に必要な機能があればScrapboxを使いたい
- Keichobot→Scrapbox
    - Scrapbox側にまとめな書き込みAPIがなく「Scrapbox形式でフォーマットするところまでやるからコピペして」になってる、ひどい
- Scrapbox→Keichobot
    - Scrapboxを書いてる最中に「ここまでの話を踏まえて会話しよう」ができるといいけどScrapbox上で動かそうとするとブラウザ拡張などを使うしかない
    - Keichobotはスマホで散歩しながら使うことを想定しているのでブラウザ拡張の選択はイマイチ
    - ページ単位でデータを取って参考にすることはできる(今気づいた)
        - ScrapboxからUserScriptでPOSTしようとすると[[CORS]]に阻まれる
            - GETだと長さが足りない
        - しかし公開プロジェクトならURLだけ渡して[[KeichobotがScrapboxから読むことは可能]]
- Kozaneba→Scrapbox
    - 埋め込む手段がないからスクリーンショットを貼るしかない
- Scrapbox→Kozaneba
    - インポートできる

