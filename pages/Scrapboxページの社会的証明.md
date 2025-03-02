---
title: "Scrapboxページの社会的証明"
---

1万ページもあるとどれを呼んだらいいかわからない問題に対して「他人が言及するものは言及する価値があるものである」と[[社会的証明]]するアプローチ
- 「他人」は「全人類」じゃないと思う
    - 下世話な芸能ニュースとか誰もが一言言いたくなるような釣りネタが選ばれてしまうから

他人のプロジェクトから自分のプロジェクトへのリンクを検索
- [https://scrapbox.io/sta/search/page?q=%2Fnishio](https://scrapbox.io/sta/search/page?q=%2Fnishio)
- [https://scrapbox.io/takker/search/page?q=%2Fnishio](https://scrapbox.io/takker/search/page?q=%2Fnishio)
- [https://scrapbox.io/blu3mo-public/search/page?q=%2Fnishio](https://scrapbox.io/blu3mo-public/search/page?q=%2Fnishio)
- [https://scrapbox.io/tkgshn/search/page?q=%2Fnishio](https://scrapbox.io/tkgshn/search/page?q=%2Fnishio)
- [https://scrapbox.io/rashitamemo/search/page?q=%2Fnishio](https://scrapbox.io/rashitamemo/search/page?q=%2Fnishio)
- ざっと思いついた「何十件もリンクがある人」
    - 1件だけリンクしてる人より信頼できるリンクのはず
        - SNSのバズで流入した一見さんではない証拠
    - そもそもTwitterでのバズとかと比べて「Scrapboxのヘビーユーザー」ってところでかなりアーリーアダプター選抜されてる

人間が見る検索ページは設定によって新着順だったりPageRankだったりする
- APIならパラメータでどちらにするのかを決められる
- [https://scrapbox.io/api/pages/sta/search/query?skip=0&sort=pageRank&limit=30&q=%2Fnishio](https://scrapbox.io/api/pages/sta/search/query?skip=0&sort=pageRank&limit=30&q=%2Fnishio)
- このAPIを使って複数のプロジェクトから集めて束ね、言及の多い順にソートして表示する
    - それぞれの人の言及リンクもセットで
    - 面白そう

初めてプロジェクトを訪れた人に見せる「まずはこの記事はどう？」はこれが良いのでは
- もしくはこのリストの中からさらに著者が選別する
- なぜなら「有益な議論を生む種」である可能性が高いから
- 現状のScrapbox、少なくとも僕のこのプロジェクトに関してはPageRank順ソートは「初めに見るのにおすすめなページのリスト」としてはまったく機能しない
    - 単独で機能しないページが多い
    - Most Viewedの方がマシだが、これは「Twitterでバズったもの」が多くなる
    - 「プロジェクトを跨いだ言及の件数」とかがオフィシャル機能として存在するといいのか？
        - いやまあでも、一人で1万ページ書くのはオフィシャルの想定ユースケースのコアとは離れた使い方か
        - 組織内のグループウェアとして使うなら「新しくチームに入った人が読むのにおすすめのページ一覧」が人手でメンテされるべきか
        - 組織の内外境界なしに関連の強い興味によって緩やかに繋がったグループのグループウェア
            - 連想 [[なめらかな社会とその敵]]
