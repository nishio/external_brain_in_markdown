---
title: "Draw.io"
---

[VSCodeでDraw.ioが使えるようになったらしい！ #VSCode - Qiita](https://qiita.com/riku-shiru/items/5ab7c5aecdfea323ec4e)
[[図解ツール]]
[[vscode]]

[【Markdown活用】Markdown文書のSVGファイルをDraw.ioでリアルタイムに編集する Visual Studio Code - システムとモデリング](https://otepipi.hatenablog.com/entry/2020/05/25/192844)
Visual Studio Codeの拡張機能であるDraw.io Integrationを使って、Markdownファイル内のSVGファイルをリアルタイムに編集する方法について解説しています。要点をまとめると以下のようになります。
1. Visual Studio Codeの拡張機能「Draw.io Integration」をインストールする
2. 任意のディレクトリで拡張子が`.drawio.svg`のSVGファイルを新規作成する
3. Draw.ioの編集画面が開くので、GUIで図形を描画する
4. 同じディレクトリにMarkdownファイルを作成し、先ほど作ったSVGファイルを`![](ファイル名.drawio.svg)`の形式で挿入する
5. Markdownプレビューで挿入したSVG画像が表示されることを確認する
6. Draw.ioの編集画面でSVGファイルを編集し保存すると、Markdownプレビューがリアルタイムに更新される

また、Draw.io Integration拡張機能はMermaid.jsにも対応しているので、通常Mermaid記法に対応していないMarkdownビューアーでもMermaid図を表示できるメリットがあることも紹介されています。

この拡張機能を使うことで、SVG画像の編集とMarkdownへの埋め込みを効率的に行うことができ、ドキュメント作成のワークフローが改善されると説明しています。Visual Studio Codeユーザーにとって有用な情報が提供されている記事だと思います。