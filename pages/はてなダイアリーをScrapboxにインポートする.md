---
title: "はてなダイアリーをScrapboxにインポートする"
---

2018年の記事。see 2021 [[はてなダイアリーを過去の日付でScrapboxにインポート]]

管理画面の「データ管理」から日記データ形式をダウンロード
![image](https://gyazo.com/60444ebf3bb68bac074789a63c2409dc/thumb/1000)

[https://github.com/nishio/hatenadiary_to_scrapbox](https://github.com/nishio/hatenadiary_to_scrapbox)
XMLから各日のデータを抜き出し、1日単位でScrapboxのJSON形式で出力する
リポジトリには参考までに入力ファイルと出力ファイルも入れておいた

そのJSONファイルをScrapboxのSettings > Page Dataからインポートする
インポートしたもの: [/test-hatena](https://scrapbox.io/test-hatena)
はてなダイアリー形式からScrapbox形式への変換はしてない