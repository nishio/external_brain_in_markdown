---
title: "Stable Diffusionのシードとプロンプトの関係"
---

同じプロンプトでも乱数シードによってこれくらい出力にランダムな幅が出る
- ![image](https://gyazo.com/8a371a254a1acabfdb6bd23d08da3b85/thumb/1000)
    - この18枚、全部同じプロンプトから生成されている
    - 構図まちまちだなと思うだろう
- これはなぜか
    - 初期値は単なるランダムな値
    - そこからノイズ除去を繰り返して「人間が意味を見出せる画像の分布」に近寄っていく
    - スタートが全然違うので辿り着いたところも全然違う
    - ![image](https://gyazo.com/8c4bf57630dab4cdd0e0de2796368568/thumb/1000)
        - この模式図では2次元で描いてるけど、実際は2万次元ある
        - なので「表面」はとても広い([[次元の呪い]])
        - ほぼすべてが表面に分布する
            - 2万次元空間の中の「人間が絵として認識しうるものの集合」の分布は我々は観測できない
            - 正規分布だと仮定するなら[[高次元空間において正規分布はほぼ超球面上の一様分布]]になる

別の視点
- ![image](https://gyazo.com/ef49b57a95f9a4a9019a508887b4f642/thumb/1000)
    - これは縦に並んでいるものが「共通の乱数シード」からスタートしたもの
    - 横に並んでいるものが「共通のプロンプト」で生成されたもの
- 世の中にはAI描画系サービスでプロンプトの試行錯誤している人たちがいる
    - シードを固定しないでプロンプトを変えて試行錯誤している人はこのような観測をする
    - ![image](https://scrapbox.io/files/6331c923f88990002370e1c0.png)
    - ほぼ乱数シードの影響で絵が決まってる
    - これを見てプロンプa〜eトとの関連を見出そうとすると訳がわからない
        - 人間はランダムな出来事にも意味を見出してしまうので、こういう「乱数シードの影響」に誤った「プロンプトとの関連」を見出してしまう人もいる
- 「シードを固定して実験するといいですよ」というブログ記事を書いている人もいる
    - シードを固定してプロンプトを変える実験をした人はこのような観測をする
    - ![image](https://scrapbox.io/files/6331c928d802d7001d8ea097.png)
    - これは先ほどの例よりは意味を見出しやすそうに見える
        - 「Eはまともな絵にならないから捨てだなー」
    - ところが同じプロンプトを別のシードで試すとこのような結果になる
        - ![image](https://scrapbox.io/files/6331c92cf86836001d73190c.png)
        - 何も知らない妻に見せたところ
            - どちらもEはなかなか良いという感想
            - 上はAとEが良くて、Eの方が好き
            - 下はA,D,Eがよく、D>A>Eの順、Eもよく描けているが顔が好みではないとのこと
        - つまり「シードを固定してプロンプトを変えて観察」しても「特定のシードにおけるプロンプトの良し悪し」を学ぶことになる
            - ランダムマップ生成のゲームで特定のランダムマップをやりこんでるようなもの
                - 他のマップでそのやり込みノウハウが有用な保証はない
                - あるシードでの「よしあし」が他のシードとは一致しないから
            - あるシードでたまたま悪い結果が出たのを見て「このプロンプトはダメだな」と判断するのは[[悲観的な勘違い]]
                - もっと他のシードで試せば「最初の1回が悪かっただけで、実は意外と良かった」となるの
                - だが、過小評価しているので「もっと試す」をしない
                - これによって成功確率の適切な見積もりができなくなっている
                    - 強化学習の文脈だと、この悲観的な勘違いをどうすれば避けられるか、探索にもっと重みを置かなければ、という話になる([[利用と探索のトレードオフ]])
- 複数シード複数プロンプトの掛け合わせをして観察すると
        - ![image](https://gyazo.com/58dadfb5bca69f105b112f852016c24a/thumb/1000)
        - Aはまあまあいいのが出る確率が高い
        - Eはめちゃくちゃ変なのが出ることもあるが、とてもいいのが出る時もある
        - Cは変なのが多い
    - みたいな感じで確率分布の差がある
    - この知識はシード固定の試行錯誤による知識よりはだいぶマシ
        - 今後のバージョンアップでは無意味になる可能性がある
        - 言語モデルによる部分、言語自体の構造を反映している部分がどれくらいあるのか
            - 今後、色々なモデルが出てくることによってわかっていくだろう
    - [[C3: Computer Created Cats]]の猫画像生成では分布を[[ベルヌーイ分布]]として[[トンプソンサンプリング]]してる([[強化学習]])
        - トンプソンサンプリングとは:
            - 仮定した分布からサンプリングして、一番大きかった選択肢を試す
            - 分散の大きいものが適切に試行される
            - Cは有用でないので自動的に捨てられ、AとEは新しい試行の対象になる
            - 試行によって増えたデータで自動的に分布形状をアップデートする

Q: トンプソンサンプリング、評価結果をフィードバックしないといけないと思うが誰がやっているのか
- A: 人間がやります。
    - 1日に1500枚くらい画像が生成されて、僕と妻がそれを見て「これはいいね、これは悪いね」とラベリングして、100枚くらいの「いいやつ」と1400枚くらいの「悪いやつ」ができる
    - その結果を元にプロンプトを改善しよう、を序盤は人間がやってたんだけど、めんどくさくなったのでw
    - 「こんだけデータあったら自動化できるだろ」って言って自動化した
    - なので現状では「いいね」と思ったら「いいねボタン」を押すだけで、いいものがより多く出てくるみたいな感じになってます
Q: いいねと思ったものに紐づいてるプロンプトをより多く試すってこと？
- A: そうです
    - 少し説明が雑なので後で補足する
    - 書いた [[トンプソンサンプリング採用の流れ]]
Q: あまりプロンプトを個別に追求して行っても意味がない？
- A: そう思います。
    - 良い絵を出したければガチャを引きまくるしかない。
    - txt2imgは結局、完全ランダムな初期値からスタートする手法ですから。
    - もっとコントロールしたいならimg2imgを使うしかないかと。
Q: 適当にやってたらなかなかいい画像に出会えない？
- A: えーと、ガチャですね
    - 何が「いい画像」かの定義がなければ「いいのが出てくる確率」は不明
    - 確率不明なガチャを引いたら、いいのが出るかもしれないし、出ないかもしれない、「運」です
    - [[良いの定義]]
Q: シードがとりうる値の範囲は？
- 単なる乱数シードなので0以上4294967296未満の整数一つ
