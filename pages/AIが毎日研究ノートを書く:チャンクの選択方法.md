---
title: "AIが毎日研究ノートを書く:チャンクの選択方法"
---

from [[AIが毎日研究ノートを書く]]

AIが毎日研究ノートを書く:チャンクの選択方法
2023-08-11
チャンクの選択方法にはいくつもの選択肢がある
- A: ランダム
- B: 最近更新されたチャンク
- C: 最近新規作成されたページのチャンク
- D: 更新日時が古いものほど確率が下がる
- E: 前回のノートでベクトル検索
1日1回自動でやるという条件であればAかDが適切だと思う
- BやCでは、人間と同じ視野で物事を見ることになる
    - 「今人間が見ているものをAIも見て、発展させてほしい」というニーズ
    - それを求めてるなら1日1回の機会を待ったりせず、明示的にAIにリクエストを出せばいい
- Eは「AIが人間と無関係に自分の関心でScrapboxを読み進めて考える」ということ
    - これは筋は悪くない
    - 問題は、素朴な実装だと同じものを繰り返し読んでしまうところ
    - 「過去に何を読んだか」を覚えておいてそれを省く的な実装が必要
    - 一方で「本当に一度読んだものは二度と読まなくていいのか？」というと、まあそんなわけないよね
        - まあ過去100件とかかな
    - 2023/8/14追記
        - 前回のノートの分量で決めたらいいんじゃないかな
        - 0ならランダム
        - たくさんあるなら、それが既存の一つのチャンク由来である可能性は低いのでベクトル検索の結果を使っても「同じものばかり」にはならないのでは
        - 前回のノートがNトークンあるとそもそも追加チャンクがゼロになる
        - 1件はランダムに入れたいね
    - 2023-08-18追記
        - > たくさんあるなら、それが既存の一つのチャンク由来である可能性は低いのでベクトル検索の結果を使っても「同じものばかり」にはならないのでは
        - そんなことはなかった
            - [[🤖2023-08-18 02:22]]でたくさん違うものを入れたが
            - [[🤖2023-08-18 02:27]]では特定チャンクへのこだわりが見られた
                - ここで単語を抽象化したら抜け出すことができた
                - [[🤖2023-08-18 02:37]]
- Aは最も実装が楽なのでこの実装で実験してみた
    - その結果、はてなダイアリーがヒットするようになったが、これが僕にとっては割と良い効果があった
    - 検索にヒットしないと価値ゼロだからというわけでインポートしてある
    - のだが、Scrapbox的なリンクがないのでScrapbox的サジェストがされることはない
    - それによって、入ってはいるがあまり活用されていない状態にあった
    - はてな記法をパースしてScrapbox記法に変えるのは面倒だからやりたくない
    - これをAIが自然言語的に解釈して、要約のメモを作ってくれる、よい「掘り返し」になる

