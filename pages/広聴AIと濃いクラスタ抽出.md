---
title: "広聴AIと濃いクラスタ抽出"
---

2025-04-23
Slackに書いたものをメモ
- 「濃いクラスタ抽出」が最初に作られてGovTech Tokyoに提案された時の資料を共有しておきます。
    - →[[濃いクラスタ抽出]]
- 今の「細分化したk-meansをしてから密度でフィルタリング」という流れはHDBSCANを試した後に作られた近似的な手法です。
- 一方でHDBSCANを今の「細分化したk-meansをしてから階層クラスタリング」と別にやるなら10000件程度の入力で追加で10分程度掛かることになり、それを許容できるかどうかというところが[[広聴AI]]が作られるときに議論になりました。
- 近似的手法ならプロセスの大部分を共通化できて追加コストなく「濃いクラスタ抽出」を実現できる、ということで、まずはその方針でやろうということになりました。
- この意思決定の背後には、当時まだ(今もだけど)「結果の良さ」を定量的に比較する方法がなく、HDBSCANで作られた「濃いクラスタ」がk-meansで作られたそれより「よい」のかどうか判断がつかなかったことがあります。
- 良いかどうか判断つかないものに追加の処理コスト10分を支払うわけにはいかないよね、という感じです。

memo
- 広聴AIは"[[濃いクラスタ抽出]]"って名前から変えた気がする
