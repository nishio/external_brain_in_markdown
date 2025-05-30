---
title: "Devinクレジット使い切り4/23棚卸し"
---

from [[日記2025-04-23]]
Devinクレジット使い切り4/23棚卸し

一昨日発注したDevinの解消が終わってないのは良くない
- 何が残っているのか
- レポート出力にかかる時間の目安を記載する機能の分析
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/11](https://github.com/digitaldemocracy2030/kouchou-ai/issues/11)
    - [https://app.devin.ai/sessions/5b6e83ea15414ec9904816fe0927c087](https://app.devin.ai/sessions/5b6e83ea15414ec9904816fe0927c087)
    - 時間の情報を収集することはできた
    - コメントの長さを収集するところでトラブル
        - example-polisがGitHub LFSなんだと思う
        - これの修正にDevinと僕が混乱した
    - 破棄する
- レポートの複製・再利用機能
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/19](https://github.com/digitaldemocracy2030/kouchou-ai/issues/19)
    - [https://app.devin.ai/sessions/a4ce26452412416d99b9e57cc3b4f607](https://app.devin.ai/sessions/a4ce26452412416d99b9e57cc3b4f607)
    - step2まで実装しないとテストしてもイマイチだなと思ったので報告を記録して先に進むことにしました
    - TODO: step2実装待ち
- 濃いクラスタ表示時にクラスタの説明文も合わせて表示する
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/24](https://github.com/digitaldemocracy2030/kouchou-ai/issues/24)
    - [https://app.devin.ai/sessions/197572bbb98a42349de7105ee06e3dd8](https://app.devin.ai/sessions/197572bbb98a42349de7105ee06e3dd8)
    - TODO: 人間のテストまち
- CSVアップロード時にそれを処理した場合のコストを表示
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/79](https://github.com/digitaldemocracy2030/kouchou-ai/issues/79)
    - 解説を書いた
- 解説ページ実行計画作成
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/111](https://github.com/digitaldemocracy2030/kouchou-ai/issues/111)
    - [https://app.devin.ai/sessions/a5f207f4b4b142a1a6fa8f6dee1efb33](https://app.devin.ai/sessions/a5f207f4b4b142a1a6fa8f6dee1efb33)
    - 実装させることにした
- week 6
    - run.shを実行させてみた
        - 手元で実行したエラーを共有して手元で直すよりDevinにやらせたほうがいい
        - [https://app.devin.ai/sessions/49473a3eeba845309eb9ad314c2dfd62](https://app.devin.ai/sessions/49473a3eeba845309eb9ad314c2dfd62)
        - なぜかいどばたの"まとめて処理"をばらしやがった
    - PR36をマージしてなかったからか
    - 36をマージしたら38はコンフリクトした
        - 直してもらおう
    - ✅
- [[Microsoft vs Cursor]]
- (実験)embeddingベースの前処理
    - [https://github.com/digitaldemocracy2030/kouchou-ai/issues/361](https://github.com/digitaldemocracy2030/kouchou-ai/issues/361)
    - [https://app.devin.ai/sessions/8e7e2042e6ea4f9cb730d7e29b4623e1](https://app.devin.ai/sessions/8e7e2042e6ea4f9cb730d7e29b4623e1)
    - これが一番大事なのではという指摘
        - そうかも
    - Devin実装中
    - 実装はできている
        - テストが必要

- レポート自動化はまだうまく言ってないな
    - [https://app.devin.ai/sessions/70bfd3924d9343f2aab67d56d431d3c4](https://app.devin.ai/sessions/70bfd3924d9343f2aab67d56d431d3c4)
    - なおさせる
- ブロジェクトの歴史
    - [https://github.com/digitaldemocracy2030/website/issues/30](https://github.com/digitaldemocracy2030/website/issues/30)
    - [https://app.devin.ai/sessions/ecbac97be5224f319573e024ba5051dd](https://app.devin.ai/sessions/ecbac97be5224f319573e024ba5051dd)
- 文字起こし清書
    - [[Scott Wu YouTube Japan 2025-04-22]]の清書、NotebookLLMであっさり成功した
    - チクチクやってた[[鼎談インタビュー文字起こし]]も同じやり方でいいのでは
    - [https://notebooklm.google.com/notebook/02536af8-acd6-4673-9915-dfd37438260f?_gl=1*1554tan*_up*MQ..*_ga*MTU0MzgwMDk5NC4xNzQ1Mzk1OTkw*_ga_W0LDH41ZCB*MTc0NTM5NTk5MC4xLjAuMTc0NTM5NTk5MC4wLjAuMA..](https://notebooklm.google.com/notebook/02536af8-acd6-4673-9915-dfd37438260f?_gl=1*1554tan*_up*MQ..*_ga*MTU0MzgwMDk5NC4xNzQ1Mzk1OTkw*_ga_W0LDH41ZCB*MTc0NTM5NTk5MC4xLjAuMTc0NTM5NTk5MC4wLjAuMA..)
- コード品質向上
    - [https://github.com/nishio/oss_weekly_reporter/pull/37](https://github.com/nishio/oss_weekly_reporter/pull/37)
    - すぐマージしないからコンフリクトしちゃった



世論地図OSS化、僕がREADMEを書くところで止まっている
