---
title: "機械翻訳したScrapboxをQuartzで公開2024-11-24"
---

from[/villagepump/機械翻訳したScrapboxをQuartzで公開2024-11-24](https://scrapbox.io/villagepump/機械翻訳したScrapboxをQuartzで公開2024-11-24)

何をしようとしているのか言語化する<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- いまScrapbox(Cosense)からの自動英訳がGitHub Actionで動いてる
- しかし翻訳後のScrapboxへのインポートでこけている
    - 時々この現象が起きるんだけど不可解だし、もうなんだかめんどくさいなー、Scrapboxにインポートするのはやめようかなー、という気持ち
    - [/villagepump/Cosenseへのimportが謎にこける問題](https://scrapbox.io/villagepump/Cosenseへのimportが謎にこける問題)の議論
- [[QuartzでObsidian Vaultを公開]]という事例がある
- [[ScrapboxToObsidian]]でScrapboxのJSONをObsidianのMarkdownに変換する事例がある
- これを組み合わせて「Scrapbox→JSON→英訳JSON→Markdown→Quartzで公開」ってやればいいのでは？と思っている


[[Quartz]]はv4になって[[Preact]]ベースになったらしい<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- まず少し調べるか
- [Welcome to Quartz 4](https://quartz.jzhao.xyz/)
- とりあえずやってみる
- Choose how to initialize the content in `/Users/nishio/quartz/content`
- │  Empty Quartz
- ◆  Choose how Quartz should resolve links in your content. This should match Obsidian's link format. You can change this later in `quartz.config.ts`.
- │  ● Treat links as shortest path ((default))
- │  ○ Treat links as absolute path
- │  ○ Treat links as relative paths
    - うーん、defaultにしておくか
- `$ npx quartz build --serve`
- 動きはしてる
次の調査
- [[ScrapboxToObsidian]]
- [/villagepump/nishio/from_scrapbox](https://scrapbox.io/villagepump/nishio/from_scrapbox)こんなのあった
    - なんかいっぱい色々書いてて未コミットの編集まであるなぁ
    - これどういう状況なの？
- [[MarkdownからQuartzで静的生成してGithub Pagesでserveする]]読んでる
- 当時でもQuartzはv4に見える
- 一方で当時はCosenseではなくScrapboxだった
Quartz
- [https://github.com/nishio/quartz](https://github.com/nishio/quartz)
- `This branch is 3 commits ahead of, 564 commits behind jackyzha0/quartz:v4`
- コンテンツの更新も同じリポジトリなのでカオス！
- `$ git pull --rebase upstream v4`
- > CONFLICT (content): Merge conflict in package-lock.json
- 564コミットもあるから全体像がよくわからん
- 自分のリポジトリとupstreamとでそれぞれ別々の更新がされてる？？
- いやー、わけがわからなくなった、無理だ
- ![image](https://gyazo.com/1102064e16a17999b6f8209610718784/thumb/1000)
    - GitHub Actionを無料のサーバレス実行環境として使うの、僕もOmoikane Embedとかでやっちゃってるし便利なんだけど、Gitはそんな用途のために設計されてないんだよな
    - 上流のOSSは当然更新される
    - 一旦このリポジトリはリネームして、新しくやり直そう
        - あー、だめかも
            - 同一リポジトリから複数forkできないってGitHubの制約
            - archiveしたらできるかな？→できない
            - 消すしかないか
            - <img src='https://scrapbox.io/api/pages/villagepump/gpt/icon' alt='/villagepump/gpt.icon' height="19.5"/>GitHub サポートに連絡して、nishio/A2023 の fork 関係を解除してもらう必要があります。
                - いやいや<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
            - renameしたものをcloneしてからdeleteする
- やれやれ
- 改めてfork [https://github.com/nishio/quartz](https://github.com/nishio/quartz)
    - 今後ここにcontentを入れないようにしたい
    - これは部品であってコンテンツホルダーではない、としたい
    - `% git submodule add git@github.com:nishio/quartz.git quartz`
- `% git clone --depth 1 git@github.com:nishio/etude-github-actions.git`
    - 最新だけとったら早いかと思いきやめっちゃ遅いな
- 疲れてきたのでまずお風呂に入る
- とりあえず自動化の前に1回走らせる
    - `etude-github-actions/nishio/data.json`は日本語版だな〜
    - 現在の英語JSONがなぜかリポジトリにないが`etude-github-actions/nishio/data_en_prev.json`が取りあえず英語JSONか
    - `tmp_0.sh`に`tasks/json_to_markdown/run.sh`って書いてある
        - `tasks/json_to_markdown`の中にGit Submoduleで[[ScrapboxToObsidian]]が入っている
        - 前回も細かい実験的作業をこれでやったんだな
tmp_1.sh

```
cp etude-github-actions/nishio/data_en_prev.json nishio.json
tasks/json_to_markdown/run.sh
```

    - quartzPagesができた
        - これをquartzからみる
        - `$ npx quartz create`
:

```
Choose how to initialize the content in `/Users/nishio/from_scrapbox/quartz/content`
│  ● Empty Quartz
│  ○ Copy an existing folder
│  ○ Symlink an existing folder
```

        - ここでsymlinkにすればいいわけだな

:

```
  2 | title: '"I can\'t shake it" and "I won\'t shake  ...
 ---------------------^
     at Object.yaml [as parse] (../plugins/transformers/frontmatter.ts:55:35)
```


fixed: [https://github.com/nishio/from_scrapbox/commit/5374c3dc25148f6c70a2ace62b4e5396f68146c9](https://github.com/nishio/from_scrapbox/commit/5374c3dc25148f6c70a2ace62b4e5396f68146c9)

:

```
Cleaned output directory `public` in 4ms
Found 20937 input files from `content` in 196ms
Parsed 20937 Markdown files in 6m
Filtered out 0 files in 4ms
Emitted 20949 files to `public` in 5m
Done processing 20937 files in 11m
Started a Quartz server listening at http://localhost:8080
hint: exit with ctrl+c
```


![image](https://gyazo.com/b992ca4584829022573d3af2cd92f756/thumb/1000)
- ガーン
- あー、これあれか、Scrapbpxのexport時にメタデータをつけてるとlineがobjectになるやつか

from [[MarkdownからQuartzで静的生成してGithub Pagesでserveする]]
- >  Github Wikiをコメントフォーム的に利用できるか？
- > 記事に対する質問や誤りの指摘をGithub Issuesにするか？
- なるほど
    - 英訳の質がイマイチなときに「このページをもっと改善して欲しい」という情報を送れるようにしようかと思ったがIssuesでいいか

:

```
Failed to process `content/Infinite sum compression using the inverse of a formal power series.md`: URI malformed
     at decodeURI (<anonymous>)
     at transformInternalLink (../util/path.ts:89:38)
     at transformLink (../util/path.ts:207:20)
     at ../plugins/transformers/links.ts:104:49
```

もうちょっと詳しいこと書いてくれてないとなおし方がわからん

あーー、ダメだー
- base64エンコードされてるURLが翻訳プロセスで壊れてるケースが無数にあるのか

無数にあるかと思ってげんなりしてたが意外と3個に収まった
- ローカルで見れた

これをえいやとGitHub Pagesで公開すればまあ公開はできる
- 翻訳の質がイマイチだなぁと思っている
    - でもそれは今でもイマイチだからいいのか
- 公開プロセスを自動化しようとすると上記のエラーを自動で解消しないといけない
    - 根本的にはリンクはリンクと判定してからタイトル部分だけの翻訳にすべき

[Setting up your GitHub repository](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository)
- これはsyncするとGitHubにpushする設計なのでコンテンツをこのリポジトリに置くことになる
    - コードとコンテンツが一括管理
    - 詳しくない人向けに提供するとそうなっちゃうし実際僕もomoikane-embedなどではそうした
    - が、コンテンツの更新でコードの更新が覆い隠されて長期的には良くない
- [Hosting](https://quartz.jzhao.xyz/hosting)
    - これもコードとコンテンツが一括管理の状態で、更新されたらbuildするGitHub Action

buildするとpublic/が作られる
- ![image](https://gyazo.com/f59f0cc8bc96cd087190a2720c10aca2/thumb/1000)
    - 前回も同じ話した気がするw
    - Component.ExplorerとComponent.TableOfContentsはもうコメントアウトしてあるのだが
    - Component.Graphかな？
    - Component.Searchかもしれない
    - Component.Graphを止めた結果
        - 54.58GB
    - Component.Searchを止めた結果
        - たいして変わらず
    - bodyの下に巨大なscriptタグがある
        - これをなんとかしないことにはどうしようもない感じ
Quartz 4.0は静的HTMLの末尾に巨大なscriptタグがあり1ページ2.5MBある。20000ページあると50GB程度になり問題である。この問題の解決方法はないか？GitHub Issuesなどがないか検索して
- <img src='https://scrapbox.io/api/pages/villagepump/gpt/icon' alt='/villagepump/gpt.icon' height="19.5"/>Quartz 4.0の生成ファイルサイズに関する問題は、GitHubでIssue `#1607`として報告されています。この中で、以下の解決策が挙げられています：
    - 主な原因
        - 最近の更新でMermaid.jsのサポートが追加され、JavaScriptがHTMLファイルに直接埋め込まれるようになったことが原因。
    - 解決策
        - Mermaidの無効化: quartz.config.tsで以下のように設定を変更することで、Mermaid.jsを無効化できます。
    - Mermaidを無効化するだけで、ビルドサイズが通常のサイズに戻ったとの報告があり、これは現在利用可能な最も簡単な解決策です。
- マジかよw<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/><img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
- 330.4 MBになったwww<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
一旦build結果のpublic以下を別リポジトリにおいてdeploy
- [https://nishio.github.io/quartz_deploy/](https://nishio.github.io/quartz_deploy/)
- 一応できた
    - なぜこれのバックリンクにこれがでるのか謎だ
        - [https://nishio.github.io/quartz_deploy/](https://nishio.github.io/quartz_deploy/)
        - [https://nishio.github.io/quartz_deploy/Tower-of-Sin-Babel](https://nishio.github.io/quartz_deploy/Tower-of-Sin-Babel)
    - [[History API]]がバグってるみたい<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
        - [quartz_deploy](https://nishio.github.io/quartz_deploy/)から[Tower-of-Sin-Babel](https://nishio.github.io/quartz_deploy/Tower-of-Sin-Babel)に移動した後ブラウザの戻るボタンを押すと、URL欄は[quartz_deploy](https://nishio.github.io/quartz_deploy/)に戻るが内容が変わらない
        - なんかおかしいなーと思ったがそういうことか<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
- なんか微妙だなぁ…

