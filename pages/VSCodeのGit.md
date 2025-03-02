---
title: "VSCodeのGit"
---

- 特に操作をしないでもgit statusの結果が左パネルに出てる
- それをクリックするとそのファイルの差分が左右分割で表示される
    - 右上にミニマップが表示される
    - 普通のコードエディタなので定義にジャンプとかも使える
- この差分はその場で編集できる
    - add -pしてハンクごとにeditするみたいなのをファイル全体を見渡しながらできる
    - 選択範囲ごとのstage, unstage, revertができる
- ステージが空の状態でコミットしようとすると全部ステージしてくれるので「コミットメッセージ書いてCmd+Enter」だけでコミットできる
- マージコンフリクトの解消もいい感じにできるらしいがまだやったことがない
    - [https://futureys.tokyo/lets-resolve-conflict-on-git-by-vs-code/](https://futureys.tokyo/lets-resolve-conflict-on-git-by-vs-code/)
- ターミナルで操作しても良い
    - vscode側が自動で最新表示に変わる
![image](https://gyazo.com/a1bcb91b5c90e2ad1d3abd477a55179a/thumb/1000)
[[vscode]]
