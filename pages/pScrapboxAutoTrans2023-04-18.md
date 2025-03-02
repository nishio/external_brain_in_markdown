---
title: "pScrapboxAutoTrans2023-04-18"
---

old title: [[pUnnamed]]
prev [[pScrapboxAutoTrans2023-03-25]] ([[pScrapboxAutoTrans]] / [[ScrapboxAutoTrans]])
- 3週間以内にまともにする
- まともとは
    - 自己紹介ページでYasukazu Nishioと訳されてるのが微妙

- 2023/4/6
    - > まずはScrapboxに自動インポートする
        - > 理想としては[[mem.nhiro.org]]につなげるのが良いが、まずは手軽な一歩から
    - > 活動ダイジェストを自動Tweetしたい
        - > まずは手軽なところから「Tweet内容をファイルに出力」「人間がそれを見てTweet」
    - 4/7
    - > Scrapbox機械翻訳結果を見て、初っ端から「Yasukazu Nishio」と訳されてるのを見てガッカリしている



2023-04-20
- 自動インポートがうまくいかなくてほったらかしの件
- `ClientResponseError: 503, message='Service Unavailable', url=URL('https://scrapbox.io/api/page-data/import/nishio-en.json')`
    - 詳細不明だからどうしようかなと
    - 今回「JSONが大きすぎるのが問題か？」となって100件に絞ってみたが同じエラーだった
- そもそもの話、[[Scrapbox-Duplicator]]のTS実装ではファイルサイズが大きすぎてエラーになる
:

```
% deno run --allow-net=scrapbox.io --allow-read=./ --allow-env import_to_scrapbox.ts
A new release of Deno is available: 1.32.2 → 1.32.4 Run `deno upgrade` to install it.
Importing 14726 pages to "/nishio-en"...
error: Uncaught (in promise) MulterError when importing pages: File too large
    const error = new Error();
                  ^
    at file:///Users/nishio/etude-github-actions/import_to_scrapbox.ts:31:19
```

- 100件に絞ってみたらいけた
:

```
% deno run --allow-net=scrapbox.io --allow-read=./ --allow-env import_to_scrapbox.ts
A new release of Deno is available: 1.32.2 → 1.32.5 Run `deno upgrade` to install it.
Importing 100 pages to "/nishio-en"...
import success! - 100 pages
```

- 前回更新時のデータを取っておいて差分だけインポートするようにするか…
    - ✅

- この問題自己紹介ページでYasukazu Nishioと訳されてるのが微妙
    - DeepLの用語集に入れるという手もある
        - 今後のことを考えるとそうするのが良い
    - しかしすでに翻訳してあるものの中にある誤訳は「すでに翻訳済みだから翻訳しないで良いな」と判定されるため、それでは更新されない
    - なのでどっちみち、誤訳を含むキャッシュを修正もしくは削除する必要がある
        - 文字列検索でマッチしたものを置換で修正した
        - たぶん大部分のケースでこれでいいんじゃないかな
    - ✅

英語話者に「これが私のScrapboxです」と示しても恥ずかしくないレベルまで持ち上げる
- それが済んだら次はベクトル検索とGPT-4との融合だ
- 僕のScrapboxのベクトル検索を誰でも利用可能にするのは優先度はそれほど高くないな？


以前Scrapboxの自動翻訳を考えてた時にはまだプロジェクト間リンクがなかった？
- 英語記事と日本語記事をどうやって対応づけるかなと思ったが、普通に自動翻訳後のページに「元ページはここ」とリンクを追加すればいいだけじゃん？となった
- ✅
    - 日本語プロジェクトにリンクを貼る時にtitleの値を使っているのだが、そうすると空白などを含む時にリンクが繋がらないので正しくエスケープすることが必要

やったー、できたー
- ![image](https://gyazo.com/a21ccd0e544bc2f7c9c609a3dfe439c9/thumb/1000)



> [@nishio](https://twitter.com/nishio/status/1649044721740967943?s=20): 死んだ！
> >batch response: This repository is over its data quota. Account responsible for LFS bandwidth should purchase more data packs to restore access.
はー、1GBの枠を使い切ってる
- とりあえず月額5ドル課金したら50GBになるようだから課金した
- ![image](https://gyazo.com/56893388970db00c70dfd786616fe94e/thumb/1000)

`ブログと違ってメインの[読者は自分]です`が`Unlike a blog, the main [reader is you].`になってる
- page titleの方は`reader is self`になってんな...

2023-04-21
- ![image](https://gyazo.com/73663a077af45b4c9f3a8e1907b48803/thumb/1000)
- 自動実行成功してた

2023-04-21
- from [/villagepump//nishio/pUnnamed(仮)](https://scrapbox.io/villagepump//nishio/pUnnamed(仮))
    - [[ScrapboxTranslator]]では↓の方法で対処して上手く行きました（失敗ケースを観測していない）<img src='https://scrapbox.io/api/pages/villagepump/blu3mo/icon' alt='/villagepump/blu3mo.icon' height="19.5"/>
        1. 先にタイトルだけ全て英訳して、日英対応テーブルを作る
        2. 本文のリンクを機械的に英語に置き換える
        3. リンクがすでに英語に置き換わっている文章をChatGPTに投げて翻訳
            - DeepLでもこれがうまくいくかは不明
        - おおー、参考になります！>失敗ケースを観測していない<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>

- A: len(cache)は22万ある
    - これはdictなのでO(1)
        - タイトルだけでなくすべての行を含んでいるがO(1)なので気にしないことにする
- B: リンク記法を抽出する
py

```
>>> re.findall("\[.*?\]", "aaa[bbb]ccc[ddd]eee")
['[bbb]', '[ddd]']
```

    - これはコード記法の中身にもヒットしてしまうが気にしないことにする
- BをAから探し、訳があるなら置換する

- あー、「読者は自分」はそもそもページタイトルですらないぞ
    - ![image](https://gyazo.com/ac0ae1b0d459104876a5d618cb9c6911/thumb/1000)
    - このパターンだ
- `api/pages/nishio/search/titles`を使ってリンクを集めた
    - 25000件ある
    - とりあえず翻訳を走らせた

2023-04-22
:

```
25321
100%|████████████████████████████████████████████████████████████████████████████████████████| 25321/25321 [4:37:38<00:00,  1.52it/s]
total 565897 no_cache 277634 ratio 0.4906087150135095
translate: 16659.303921374958
```


:

```
>[https://twitter.com/tkihira/status/1269780950105206787?s=21 @tkihira]: 「スーパーエンジニアへの道」という[ワインバーグ]の名著で、新しい技術を習得するときの[実力の一時的な低下]とどう向かい合うか、という話が紹介されていて、自分の中でも重要な話として強く記憶されている。
['https://twitter.com/tkihira/status/1269780950105206787?s=21 @tkihira', 'ワインバーグ', '実力の一時的な低下']
>[https://twitter.com/tkihira/status/1269780950105206787?s=21 @tkihira]: 「スーパーエンジニアへの道」という[Weinberg]の名著で、新しい技術を習得するときの[Temporary decline in competence]とどう向かい合うか、という話が紹介されていて、自分の中でも重要な話として強く記憶されている。
```

うまく訳せるかどうかは運

とりあえず今日明日は忙しいので、これで走らせておく

2023/4/22
- 第三の案
    - 行からリンク記法を取り除いてプレーンテキストとして翻訳し、その結果に「リンクの中身を翻訳したもの」が含まれるならそこをリンクに変換、含まれないなら末尾につける

2023-04-23
:

```
%run translate.py
cache length: 229791
100%|████████████████████████████████████████████████████████████████████████████████████████| 14760/14760 [7:17:20<00:00,  1.78s/it]
total 29581111 no_cache 2492102 ratio 0.08424639628984862
translate: 26244.572622375097
```

約8パーセントの再翻訳で済んだようだ
- よくなったかどうか定量的に判断したいなぁ

インポートに失敗した
- ![image](https://gyazo.com/c8e644535d2db56c52756cdc39430dd9/thumb/1000)
- やり直したらいけた
- 謎

2023-04-27
![image](https://gyazo.com/1292dbb0f3f52d08894785c58d8b4460/thumb/1000)
works well
[[Continuous Translation]]
next: [[pContinuousTranslation2023-04-27]]
