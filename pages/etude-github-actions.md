---
title: "etude-github-actions"
---

[https://github.com/nishio/etude-github-actions](https://github.com/nishio/etude-github-actions)

2023-11-17
Github Actionのことを全然知らなかったので練習のつもりで作った
- etude(エチュード)とは楽器の演奏スキルの修得を目的とした曲のこと
- ところがそこで実験していた[[Github ActionsでのScrapbox自動翻訳]]が思ったよりうまく行ったのでそのまま運用フェーズになった
    - この結果、時間が経ってから「あれ？翻訳機能ってどこで動いてるんだ？」となってしまった

- 4/20 [/villagepump/nishio/pUnnamed(仮)](https://scrapbox.io/villagepump/nishio/pUnnamed(仮))
    - 当時は"pUnnamed(仮)"と呼ばれてた、酷いw
    - 後に[[pScrapboxAutoTrans2023-04-18]]と呼ばれるようになった
        - この[[pScrapboxAutoTrans]]自体が、のちに[[pContinuousTranslation]]になり、そして[[pEnglish]]になった
            - [[翻訳ではなくブログ文章生成]]などの議論により「翻訳(Translate)と呼ぶことは視野狭窄の原因になる」と思ったから

- 10/12 [/villagepump/作業室2023-10-12](https://scrapbox.io/villagepump/作業室2023-10-12)
    - > 過去のコード、どこ？…見つからないと思ったら「練習」の中にあったw
    - 酷いw
    - > 訳の良し悪しを議論する場が必要
    - > 非エンジニアの日本人が使える必要がある
    - これは[[pPluralityBook]]の話

- 11/13~
    - [[読者AIを作る]]

何をやっているか解説
- DenoとPythonの環境を作る
- DenoでScrapboxからJSON exportする
- [[DeepL API]]で翻訳する
    - [https://github.com/nishio/etude-github-actions/blob/main/translate.py](https://github.com/nishio/etude-github-actions/blob/main/translate.py)
- 前回のJSONとのDiffを取る
    - importに失敗することがあり(A)、JSON全体ではなく更新差分だけにしてみた
    - [https://github.com/nishio/etude-github-actions/blob/main/diff_json.py](https://github.com/nishio/etude-github-actions/blob/main/diff_json.py)
    - なぜこうしてるかというと、特に開発序盤はシステムの変更にやって元データの更新なしに訳文の変更などがあったから更新日時でのフィルターを入れてなかったから
- 最新のJSONと翻訳済みJSONをコミット
- 翻訳差分JSONをScrapboxにimport
    - ここで謎にコケることがあり、原因がわからなかったのてPython移植を試みたが、結局差分更新で解決した




表記揺れ [[github-action-etude×]]

[/blu3mo/Scrapbox Translator v3](https://scrapbox.io/blu3mo/Scrapbox Translator v3)

