---
title: "MarkdownからQuartzで静的生成してGithub Pagesでserveする"
---

from [/villagepump/MarkdownからQuartzで静的生成してGithub Pagesでserveする](https://scrapbox.io/villagepump/MarkdownからQuartzで静的生成してGithub Pagesでserveする) 2023-11-30

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>以下は要約です：

### Markdownから静的サイトを生成してGitHub Pagesでホスティング
変換と生成:
- Scrapbox JSONからMarkdownに変換 ([[from_scrapbox]] ([https://github.com/nishio/from_scrapbox](https://github.com/nishio/from_scrapbox) ))
- Quartzを使用して静的サイトを生成 ([[Quartz]]( [https://quartz.jzhao.xyz/](https://quartz.jzhao.xyz/) ))
- frontmatter追加が必要で、Obsidian形式への調整が課題。

課題と対応:
- 元データやMarkdown構造の修正。
- Wikilinks対応やプラグインの調整。
- QuartzのExplorerプラグインの欠点を解消（ページリンクの肥大化問題）。

デプロイ:
- GitHub Pagesを使用してデプロイ。
- ファイルサイズ制限（1GB）やビルド時間制限の問題を解決。
- 不要なリンク削除でビルド時間を短縮。

最終的に成功し、静的サイトのホスティングが完了：[https://nishio.github.io/quartz/](https://nishio.github.io/quartz/)

