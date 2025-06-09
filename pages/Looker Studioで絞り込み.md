---
title: "Looker Studioで絞り込み"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Looker studioでユーザがグラフの元データの都道府県の値を切り替えてフィルタした結果を見れるようにできる？
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
1. ドロップダウンリスト（推奨）
- データソースに都道府県列（Dimension）があることを確認
- レポートを編集モードで開き、ツールバーの 「コントロールを追加」 → 「ドロップダウンリスト」 を選択
- 右側のプロパティ > Control field に「都道府県」を指定
- 「複数選択を許可」や「検索ボックスを表示」など、好みに応じてオプションを設定
- 既定では同じページ上の全チャートが対象になりますが、「Apply filter to」 で特定チャートのみに作用させることも可能
これで閲覧者はプルダウンから都道府県を選ぶだけで、該当データに絞り込まれたグラフを確認できます。

![image](https://gyazo.com/05177f9e98b3cbc68a6fd792fb461693/thumb/1000)
- できた<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
    - [[Looker Studio]]便利だな
    - 聞いたら教えてくれるChatGPTも便利

[[チームみらい都道府県別ボランティア登録者]]
