
from [/villagepump/ScrapboxプロジェクトをKozanebaにインポートする(開発)](https://scrapbox.io/villagepump/ScrapboxプロジェクトをKozanebaにインポートする(開発))
サクッとできる話ではないことがわかったので思考過程をここに置いていく<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>

Kozanebaのサンプルコードで「ソースコードからKozaneba用のJSONを作成する」があるので、これを使ってScrapboxからエクスポートしたJSONからKozaneba用のJSONを作ればいいと思った
- エスクポートしたJSONにはリンクの情報がなかった

前提として「ページの間のリンクをKozanebaの矢印としてインポートする」という仕様
- 線のないバラバラの要素としてから今でもできる

各ページのAPIを叩いてリンク情報を取得する？
- リンク情報付きでページ一覧が得られるAPIがあったはず<img src='https://scrapbox.io/api/pages/villagepump/inajob/icon' alt='/villagepump/inajob.icon' height="19.5"/>
    - [/scrapboxlab/api/pages/:projectname/search/titles](https://scrapbox.io/scrapboxlab/api/pages/:projectname/search/titles)
    - でもこれだと本文がない
    - エクスポートしたJSONから作るケースなら手元に本文はある<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
        - というかKozaneba的には本文は使わないな
            - そんなことなかった、まあいいや
            - UI経由で追加した時にはその時点でAPIを叩いてdescriptionを取得してる
            - 一旦descriptionを空でやる
                - 後で考える
    - これで良さそう
    - 先日inlineに井戸端補完機能をつけるときに使ったばかり
    - レスポンス眺めてみた、これで良さそう<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>
    - 赤リンクも含まれるはず、まぁあっても良いか<img src='https://scrapbox.io/api/pages/villagepump/inajob/icon' alt='/villagepump/inajob.icon' height="19.5"/>
        - あった方が面白いかない方がいいかは不明<img src='https://scrapbox.io/api/pages/villagepump/nishio/icon' alt='/villagepump/nishio.icon' height="19.5"/>

とりあえず100ページ程度のプロジェクトを対象に実験しようとしているので、全ページ対象で良い
- が一般的にこの機能がリリースされた時に使ってみようとする人は10000ページあったりするので全体でやっても[[毛玉問題]]になるだけ
- ページを指定して、そのページと1ホップでリンクされているのものだけを対象にするのが一番有用だと思う
    - 100リンク超えてしまったようなページを指定して読み込む
    - そうすると子のページの間のリンクが見えて、子をグループに分ける助けになる
    - このユースケースだったら親から子へのリンクは自明だから描かない方がいいな

有用かどうかはさておき面白いかもしれないこと
- 指定したページ(orランダムページ)からランダムにリンクをたどっていくのを100回くらいやった結果を表示

[/scrapboxlab/api/pages/:projectname/search/titles](https://scrapbox.io/scrapboxlab/api/pages/:projectname/search/titles)
- タイトルはある
- 画像URLはある
- 本文はない
- このページ自体のURLはない
    - スペースの置換とURLエンコードをすればいいかな？
- リンク情報はリンク先のページタイトルになってる
方針
- 大した分量ではないので素直に頂点集合と辺の集合をつくる
- 有向辺にするかどうか
    - するのはできるけど双方向のやつをどう表示しようかな
    - 両矢印でいいか
- 赤リンクを含むためページ一覧に存在しない端点が発生しうる
    - 赤リンクの先をこざねとして追加しよう

赤リンク、予想以上に多かったw
- ![image](https://gyazo.com/6ae926fccbf166fc262b27369345056d/thumb/1000)
    - 赤リンクをインポートするのはやめます

さて...
- ![image](https://gyazo.com/58d2bdca9ff75cb0dedd5a34949a0996/thumb/1000)
- 実は物理エンジン実装してある
    - ![image](https://gyazo.com/9d1baef134a404e4f21f2fece6cea622/thumb/1000)
    - あんまり役に立ったことがないので公式ドキュメントにはないw

- うーん、人類はこの毛玉問題を解決する手段をまだ発明していない…
    - ![image](https://gyazo.com/9b479212a7920bf6eb07dec777d861cb/thumb/1000)
    - 孤立してるものを傍にどけたり、1つとしかつながってないものをそれのそばに置いたりするところまでは自明
    - そこから先が急に難問になる
        - 数百枚でのKJ法経験が何度もある僕にとってすら、この100枚のカードの毛玉を解きほぐすのに困難がある
    - 巨大なハブになってる雑談ページをリンクから外そう
    - あ、Scrapboxこざねにleave from linesメニューがついてないぞ…
    - まあインポートはできたし続きはまた明日
    - あ、そうか、cloneして削除で同じことできるな
        - Scrapboxこざねにcloneも付いてないじゃん！

メモ
- ページ99枚
- リンク400本

