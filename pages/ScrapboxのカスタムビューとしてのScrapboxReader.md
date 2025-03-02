---
title: "ScrapboxのカスタムビューとしてのScrapboxReader"
---

from [/villagepump/ScrapboxのカスタムビューとしてのScrapboxReader](https://scrapbox.io/villagepump/ScrapboxのカスタムビューとしてのScrapboxReader)
![image](https://gyazo.com/7ae3f64d6fd65a1aa62cab01dcd53806/thumb/1000)

Scrapboxの[[カスタムビュー]]としての[[Scrapbox Reader]]

ジャストアイデア<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- Scrapbox上で「これはScrapboxReaderのための指示だな」と人間が見て分かる文字列を書く
- 箇条書きの子要素はパラメータだったり、人間のためのコメントだったり、ScrapboxReaderへのリンクを置く
- ScrapboxReaderの側ではScrapboxのデータをAPI経由で受け取ってレンダリングする
    - このときにどうレンダリングするのかの指示する文字列があるか見て、あればそれに従ってレンダリング方法を選択する
- ScrapboxReader自体では編集はできないが、常にわかりやすい位置に元のScrapboxページへのリンクがあるなら「編集ボタンをクリックして編集」と大して変わらないので慣れることができると思う
- 「UserScriptを入れれば入れた当人だけ使える」というタイプのカスタマイズと比べて
    - Scrapboxオリジナルのレンダリング結果を使えないので手間
    - Scrapboxオリジナルのレンダリング結果に依存しないので物によっては実装が楽
        - 壊れにくさ
    - 作ったものを「こんなものを作った」と人に見せることが容易
