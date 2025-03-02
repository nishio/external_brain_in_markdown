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

--- raw

2023-11-30
のりしろ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- Markdownは[[nishio/from_scrapbox#655cbb2caff09e0000e993e0]]でScrapbox JSONから変換してる
- 静的生成には[[Quartz]]を使っている
    - [[Quartzでの静的配信]]

from [[nishio/from_scrapbox]]
- MarkdownからStatic Siteを生成してGithub Pagesでserveする
- <img src='https://scrapbox.io/api/pages/nishio/blu3mo/icon' alt='blu3mo.icon' height="19.5"/>の[[QuartzでObsidian Vaultを公開]]を参考にする
    - reading...
    - [[Hugo]]が使われている？言語はGolang？
        - [https://gohugo.io/documentation/](https://gohugo.io/documentation/)
        - [https://quartz.jzhao.xyz/](https://quartz.jzhao.xyz/)
            - > Quartz requires at least Node v18.14 and npm v9.3.1 to function correctly.
                - あれ？Nodeだな
    - Obsidian形式からQuartz形式にするのにfrontmatter付与の軽い変換が必要なのか
        - [https://quartz.jzhao.xyz/authoring-content](https://quartz.jzhao.xyz/authoring-content)
            - aliases, tagsがある
            - 最低限titleだけでいいのかな
            - 現状ScrapboxToObidianで作られたMarkdownにはタイトルの情報はない
                - ファイル名に入れてある
                - 大丈夫？情報失われてるやつとかない？？
                - `page["title"].replace(/\//gi, "-")`
                - ふうむ、Obsidian形式の出力が欲しいわけでない場合、[ここ](https://github.com/nishio/from_scrapbox/commit/0cb3ebf89bfe923099daba08e09e83cc10c7e1f1)で分岐する方がいい気がするな
    - [https://quartz.jzhao.xyz/features/wikilinks](https://quartz.jzhao.xyz/features/wikilinks)
        - ObsidianがWikilinksをサポートしてて、Quartzも同様にサポートしてるということか
- <img src='https://scrapbox.io/api/pages/nishio/shoya140/icon' alt='shoya140.icon' height="19.5"/>の[[井戸端日記帳]]はNext.jsから生成していた
    - こちらは自由度が高そう
    - Quartzのこと詳しくないけど、これくらい手軽にカスタマイズができるといいな
- 検討
    - Github Wikiをコメントフォーム的に利用できるか？
        - 少なくともWikiには誰でも書き込めるようにするオプションがある
    - 記事に対する質問や誤りの指摘をGithub Issuesにするか？
- とりあえず動かす
    - Nodeが古いと言われて入れなおし
    - ![image](https://gyazo.com/d70ad0a72627036c89a0031649517031/thumb/1000)
    - ![image](https://gyazo.com/2d059ae2da054bad7d2c61403717d6b9/thumb/1000)
    - うーん
    - ![image](https://gyazo.com/82353ebe17bb306ad10ca28430561a4e/thumb/1000)
    - これは元データがゴミ [[2020-01-16]]
    - [直した](https://github.com/nishio/from_scrapbox/commit/462310104e18003121685272ea28c7f3a43980ca)
- ![image](https://gyazo.com/12627f7106e6ca3ef28f7b216c63df1f/thumb/1000)
    - どう見てもdivとstyleの間に空白が足りないというアホなミスだがどこを直せば良いのかわからんな
    - ![image](https://gyazo.com/f2ab19599bbdf51a769ab94fed42e3ac/thumb/1000)
        - あー、元データか
- ![image](https://gyazo.com/9f30f00bbee59351ff3aab1c284d9d5b/thumb/1000)
    - 20分掛けてなんとかなったっぽい、警告出てるけど。
    - ![image](https://gyazo.com/39ab4df38bad311978fbf02f2f64f29c/thumb/1000)
    - index.mdがないから404だw
- ![image](https://gyazo.com/656074928e4a7a3223c28faf892be76a/thumb/1000)
    - 一応ちゃんと表示されてそう
    - なお左のExplorerも右のBacklinkもABC順のようだ
        - もっといい順番にしたいね
        - まあそれは0→1ではなく改善なので後回し
デプロイを調べる
- はー、なんかややこしいことしてるな
    - [Hosting](https://quartz.jzhao.xyz/hosting)
    - トリッキーな詳細隠蔽が行われてる
- どうしようかなあ、これめんどくさいぞ
- 今日は全然歩いてなくて運動不足なのでとりあえず散歩しながら考える
- 眠い、今日の活動限界が近い(もう過ぎてるかも)
- 説明の通りにしても説明の通りにならないのでは？と思ってるけど、とりあえず説明の通りにやっておくか
- なお現状
bash

```
% git status
On branch v4
Your branch is up to date with 'origin/v4'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    content/.gitkeep
        modified:   package-lock.json

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        content

no changes added to commit (use "git add" and/or "git commit -a")
```

- 手順
    - > Head to “Settings” tab of your forked repository and in the sidebar, click “Pages”. Under “Source”, select “GitHub Actions”.
    - しれっと"forked"って言ったな
    - `$ git remote rename origin upstream`
    - `$ git remote add origin https://github.com/nishio/quartz.git`
    - これでいいのかな
- Github Pagesの設定をforkしたquartzリポジトリでやる
    - ![image](https://gyazo.com/d0b529d43787e3bf540daea9b1b6517a/thumb/1000)
- これでデプロイができた(Github Action上で再度ビルドからやっている)
- で、やりたいことはそうじゃないんだよなー
    - まあでも、リポジトリが分かれててもとりあえずいいか
- Deployできてないじゃん！
    - >  System.IO.IOException: No space left on device : '/home/runner/runners/2.311.0/_diag/Worker_20231129-132926-utc.log'
    - 何がそんなに大きいんだ
    - ![image](https://gyazo.com/57f9426d7af9d04e2803d0780e652d15/thumb/1000)
    - え、どうしようもなくない？？
    - > Published GitHub Pages sites may be no larger than 1 GB. [About GitHub Pages - GitHub Docs](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)
    - Cloudfrare Pagesだと？
        - > Builds will timeout after 20 minutes. [Limits · Cloudflare Pages docs](https://developers.cloudflare.com/pages/platform/limits/)
        - これは多分引っかかるな...
    - ほぼ中身のないページですら1ページあたり2.4MBある
        - `Component.DesktopOnly(Component.Explorer())`
        - これを消すか
        - 消したら20分以上掛かってたビルドが2分で終わるようになった
        - 結論、このプラグインの実装が1万ページあるユーザを想定できていないということ
            - 全ページに全ページへのリンクを埋め込むので2乗のオーダーでファイルサイズが膨れる
    - できた！ [https://nishio.github.io/quartz/読者向けLinks](https://nishio.github.io/quartz/読者向けLinks)

