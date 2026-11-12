---
title: "grasp-nishio"
---

[[grasp]]を使ってnishioのあらゆるものを包括的に参照可能にしようとしている
2026-08-21
- >  ~/.grasp/grasp.sqlite(400MB)。← これが本体。nishio Cosense 25,897ページ + wiki森 + considerations を全部索引したローカルSQLiteグラフ。grasp read/search/related はこれを引く。

2026-11-10
- MacBookが単一の窓口とみなせなくなってきた(関連: [[デスクトップ期]])
    - <img src='https://scrapbox.io/api/pages/nishio/grasp/icon' alt='grasp.icon' height="19.5"/>GitHub の repo を入口の実体にする: どの入口で相談を受けた AI も、最初に pull して overview・rules・LOG の先頭を読み、最後に書き戻して push する。MacBook の VS Code はそうした入口の1つ、という扱いになります。
- file backのskillを修正
    - wikiによっては編集が複数マシンで行われるので、commitしたら人間に確認せずに即座にpushするべき
    - いままでは「人間に確認してからpush」だった
    - この事情はWikiによって異なるのでskillに「人間に確認してからpush」と書くのをやめて、wiki毎の指示に従うようにした

2026-11-11

