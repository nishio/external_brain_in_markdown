---
title: "Scrapbox「で」検索"
---


<img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>
- Scrapboxの問題を解決するために、ChatGPTとベクトル検索を活用し、自分のScrapboxを含むデータベースで関連情報を提供する。
- 要約:
    - Scrapboxに機械的にページを流し込む問題点
        - トップページの更新順カード一覧が見にくくなる
        - 活用がしにくい
    - 解決策
        - 古い日時でインポートし、トップページ汚染を避ける
        - 検索でポジティブ効果
    - ベクトル検索: キーワード指定なしで検索可能
    - ChatGPT利点: 関連記事を機械が要約
    - Scrapbox ChatGPT Connector利用法: AIが関連ページや要約を提供
    - 検索対象: 自分のScrapboxだけでなく、他のブログや書籍も含むデータベース
    - 検索方法変更: 質問文で検索から、自分のScrapboxの1ページでデータベースを検索する形へ

from [/villagepump/2023/03/31](https://scrapbox.io/villagepump/2023/03/31)
- Scrapboxに機械的にページを流し込むとゴミ屋敷になる論
    - たしかに、流し込んだものがトップページの更新順カード一覧に表示されるとイマイチ
    - しかし古い記事を古い日時をつけてインポートするのはトップページを汚染しない
    - 検索の時にヒットするのでポジティブな効果がある
- ここまでが「今までの考察」
- [[ベクトル検索]]によって
    - 明示的にキーワードを指定しなくても[[「今書いている文章」で検索]]できる
        - これだけでは「関連記事のレコメンド」と変わらない
- ChatGPTで「その関連記事を人間が読むのではなく、機械が読んで要約する」ができるようになった
    - ここがすごいところなのでは
- つまり「機械的に流し込んだコンテンツは連想のリンクが貼られていないからその後の活用がしにくい」という問題を解決するのでは
- [[Scrapbox ChatGPT Connector]]で「質問できるようになる」という見え方にフォーカスしたのは間違いで、むしろ「自分がScrapboxで書いたページに対して、AIが『関係ありそうなページ』とか『要約』とか『どうして関連があると思ったか』をつけてくれる」という使い方の方がいいのでは
- この検索対象が自分のScrapboxである必要はない
    - 他のサービスでブログ書いてる人のブログ記事とか
    - 書籍とか
- 整理すると「『質問文』で『自分のScrapbox』を検索する」という形から「『自分のScrapboxの1ページ』で『自分以外のものも入ったデータベース』を検索する」という形
    - [[他人のScrapboxもベクトル検索したい]]
