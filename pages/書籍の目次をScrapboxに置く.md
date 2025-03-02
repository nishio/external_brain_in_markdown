---
title: "書籍の目次をScrapboxに置く"
---

from [[井戸端2022-01-20]]
書籍の目次をScrapboxに置く
- 書籍の目次をScrapboxに置く場合、どうするのが良いのか
    - ユーザの利便性からすると、書籍同様に小見出しまで全部展開されていて、クリックするとそこにジャンプするのが好ましい
    - が、Scrapboxの[[対称なリンク]]でそれをやるとすべてのページが目次をハブにしてつながってしまう、これはScrapbox的に良くない
    - 仕方がないから章、節、項…とそれぞれの階層をページにしてみたんだけど、見通しも悪いし全然ダメな気がする
        - [/nishio/Root of the book](https://scrapbox.io/nishio/Root of the book)
    - 普通の書籍みたいに箇条書き展開表示にして外部リンク記法で片方向リンクを張るかな…

from [[井戸端2022-01-23]]
書籍の目次をScrapboxに置く
- 書籍的ナビゲーションをやる上で問題なのは「片方向リンクがない」ではなく「2ホップリンクされてしまう」
    - どういうことか
    - 「目次から各ページにリンクをしたら巨大なリンクになる！」
        - これは「それが目次というものの役割だ」
    - 「目次から各ページにリンクしたら、各ページにからも逆リンクが発生する！」
        - 逆リンクが目次ページに対してだけ発生するならなんの問題もない、むしろ便利では？
    - 問題の本質は「各ページから目次ページを介して他のすべてのページに2hopリンクが生まれること」
        - そして小さいリンクを優先表示したりしないと「大きなリンクがすべてのリンクを覆い隠す」
        - いや、目次ページから各ページにしかリンクしていないのだとしたら、[[2 hop link]]は生まれないはずです<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
            - ![image](https://i.kakeru.app/7df83435ec8f3f659c524dc114bb76c1.svg)
            - [[階層構造型のリンクは2 hop linkになら]]ないと表現しておくか
        - 2 hop linkになるのは各ページから目次ページリンクが貼られているとき
            - ![image](https://i.kakeru.app/cdd09c3746dbfd10d63a0d172f679898.svg)
        - なんと！知らなかった！<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
            - Scrapboxのリンクの概念難しすぎる
            - ![image](https://gyazo.com/125d983f24f4d3a08e7b21d15da83fe0/thumb/1000)
            - ほんとだー
            - 確認ありがとうございます
                - あっててよかった
    - なので目次ページを作るのは逆にアリですね<img src='https://scrapbox.io/api/pages/villagepump/takker/icon' alt='/villagepump/takker.icon' height="19.5"/>
        - やってみたけどよさそうです
            - [/nishio/(0.1.2) Benefits of reading this book](https://scrapbox.io/nishio/(0.1.2) Benefits of reading this book)
            - Table of Contents経由の2hopリンクが作られない
        - 本当は各ページの側にも[[ブレッドクラム]]を付けようかと思ってたんだけどそれは保留することに(やるとしたらそっちだけ片方向リンクにするとかかな)
            - [[2 hop linkを無効に]]
                - あーなるほど、別タブで開いてしまうのか…
                - まあビューに関しては公式の実装で自分のニーズが満たせるとは思ってないのでカスタムビューでいじる方針
