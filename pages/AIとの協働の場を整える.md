---
title: "AIとの協働の場を整える"
---

いままで「一人でコードを書いて実験する」的なキャリアがメインだったので複数人プロジェクトでそれぞれが開発した時値formatterの違いによってdiffが大きくなる問題をあんまり体験してこなかった
- 何年も前のVSCode導入時にデファクトっぽいformatterを入れてfotmatOnSaveにした気がする、ぐらいの感じ
- 複数人プロジェクトに参加する時には誰か自分以外の人が設定をしていることが多かった
- だがしかし[[Devin]]を使うようになって、人間が自分一人しかいなくてもformatter統一をやることが必要になった

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
- Black（デファクト）、Ruff format（高速＋lint一体型）など、どれでもいいので「全員が同じバージョン」を使うと決める。
- プロジェクト直下の pyproject.toml に設定を置き、IDE 依存の設定は最小化する。
- まず全ファイルを一度だけ一括整形してコミット
    - フォーマット専用の単独コミットを切ると、その後の PR ではロジック変更だけが diff に現れるようになります。
- 開発環境を合わせる
    - リポジトリに .vscode/settings.json を入れて共有（VSCodeユーザが多いなら効果大）。
    - 他のエディタ勢がいる場合は .editorconfig も置いておくと行末・インデントは揃います。

BlackもRuffも知らなかった。もうautopep8とかじゃないんだな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
広聴AIでRuffが使われているので同じでいいや

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>いま自分のVSCodeがどうなってるかどうやったらわかる？
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>⌘/Ctrl + Shift + P → Format Document With... を実行
ポップアップに「既定 (default)」と表示されている拡張機能名が、保存時フォーマットに使われているツールです

Blackだった！<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

`$ ruff format .`
これでいいのかな

[https://chatgpt.com/c/68145ac2-8a58-8011-9937-43789ecdc38b](https://chatgpt.com/c/68145ac2-8a58-8011-9937-43789ecdc38b)

