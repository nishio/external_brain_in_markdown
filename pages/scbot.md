---
title: "scbot"
---

2018-06-05
チャットにボットを入れたりするのが流行りだが、Scrapboxにボットを入れたい
- scbotがScrapbox上で生活しているのを眺めたい
    - 餌(情報)を与えて反応を眺めたい
    - [[チャットボット]]は同期的なイメージがある
        - ユーザの入れた入力に対して[[リアクティブ]]に反応する
        - 非同期的に勝手に色々活動しているのを眺めたい
- 有益な活動ができるようになったら自分のScrapboxに接続したい
    - 単なる雑用係ではない
    - ボットの個人プロジェクト内で、[[自発的]]に有益な知的生産ができるようになってから合流したい
        - 有益な[[知的生産]]活動とはなんであるか
            - 頭を使って、新しいものを、アウトプットする

実装
- [[機械がScrapboxを読む]]
- [[機械がScrapboxに書く]]



---過去ログ
- 書き込むのに[[Puppeteer]]を使って1行1行入力するしかないと考えていた(2018)
- JSONをインポートさせる方法で[[blu3mo]]が実現した(2021)
- Puppeteer必要なかった [Use Deno and Remove Puppetter by takker99 · Pull Request #6 · tkgshn/scrapbox-Duplicator](https://github.com/tkgshn/scrapbox-Duplicator/pull/6/commits/09e4d201631bd7e8192b111bb3b5ad27577eb4d6)
- [[PythonでScrapboxにimport]]

書き込む
- 難しい
    - APIがないし、APIを用意することが開発者の哲学に合わないので用意される見込みもない
- ブラウザ操作自動化でやるしかない
- [[Puppeteer]]でHeadless Chromeを操作するか
    - [Puppeteerを使用したHeadless Chromeの操作 - Start Today Technologies TECH BLOG](https://tech.starttoday-tech.com/entry/puppeteer)
    - [GoogleChrome/puppeteer: Headless Chrome Node API](https://github.com/GoogleChrome/puppeteer)
- [Herokuを使ってchromeでwebページのスクリーンショットをとる](https://qiita.com/isamua/items/c6a2f2ae5e2b03ebca6e)
    - [[Heroku]]で[[Headless Chrome]]やってる人がいる
- 多分だけど、複数行まとめての短時間での更新が発生してそれがコンフリクトした場合がめんどくさいんだと思う
    - Scrapbox運営が書き込みAPIを実装したくない理由
- プログラムが書き込む時も1行1行心を込めてウェイトを入れて書き込むのが良さそう


書き込まない方法での伝達
- 以前UserScriptでページ出力するものを作ったら、その自動生成ページをあとで削除しないといけないのが面倒だった
    - [[自動生成ページを自動削除する]]
- [[Scrapboxはフローの場ではなくストックの場]]だからそういうものを書き込むべきでない、Slackなどに流すべき、という考え方が一案
    - そういうのを書き込むことも含めてScrapboxでやった上で、削除も実装すれば良い、がもう一案

[[チャットボット]]
