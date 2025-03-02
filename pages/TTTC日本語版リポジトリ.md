---
title: "TTTC日本語版リポジトリ"
---

UIを変えた程度のものを別リポジトリで公開するのは面倒だったのでパッチの形で公開した(2024-07-17)
- [東京都知事選2024におけるTalk to the Cityの活用ノウハウ｜NISHIO Hirokazu](https://note.com/nishiohirokazu/n/n0661204bda5b)

だがその後いろいろな環境での応用をやっていく上でリポジトリの形で公開した方がいいかもなと思ってきた(2024-09-19)

日本語用のサンプルデータとして[[人生の選択肢を知ったきっかけをTTTCする]]をやればいいのでは

リポジトリはfork済みだった
- [https://github.com/nishio/talk-to-the-city-reports](https://github.com/nishio/talk-to-the-city-reports)
- いくつかpull reqして、一部は修正待ちだった

- This branch is 2 commits behind AIObjectives/talk-to-the-city-reports:main.
    - これ僕のpull reqがマージされたよってことだな
    - ![image](https://gyazo.com/14318bc27a665b0e927d69241957b830/thumb/1000)
    - ああ、これを押せばいいのか

ここに本家にpushしない`japanese`ブランチを作ればいいのかな〜
- UI日本語化patch
- 日本語サンプルプロンプト
    - 毎回「あんのチームの公開したやつを使って」というのは微妙
- 日本語サンプルデータ
    - これはなくてもいいかもな〜
- 将来的には分析部分に日本語形態素解析
    - [[TTTC:形態素解析]]
