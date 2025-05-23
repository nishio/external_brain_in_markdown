---
title: "pKeichobot"
---

[[聞き出しチャットシステム]]に関するプロジェクトメモ

from [/villagepump/自分がWikiを作る理由](https://scrapbox.io/villagepump/自分がWikiを作る理由)
- Scrapbox→Keichobot
    - Scrapboxを書いてる最中に「ここまでの話を踏まえて会話しよう」ができるといいけどScrapbox上で動かそうとするとブラウザ拡張などを使うしかない
    - Keichobotはスマホで散歩しながら使うことを想定しているのでブラウザ拡張の選択はイマイチ
    - ページ単位でデータを取って参考にすることはできる(今気づいた)


--- old memo 2021
2021-08-20 [[KeichoからKeichobotにリネーム]]

- [[聞き出しチャット使い方サンプル]]
- [[聞き出しチャットシステム会話ログ]]
- [[聞き出しチャットシステムリリースノート]]

Scrapboxでカンバン
- WIP
- HaveBetter
    - [[🤔Scrapboxエクスポート時のフッタを指定可能にする]]
    - [[Dynalist]]
    - [[□解説のスクリーンショットを取り直す]]
    - 会話が別れる現象
        - [[謎のログが途切れるバグが起きたので相談したい]]
    - 他のキーワードを取らない質問を能動学習でスコアを決めるようにする
        - 具体的には何？
        - それから[[終わりのデザイン]]
        - [[能動学習のうまくいかない話をしてたら本を読めという結論になった]]
    - [[🤔タスク管理チャットボット]]
    - [[🤔画面高さとバーチャルキーボードの問題]]
    - standaloneの「ホーム画面に出す」をした時にローカルストレージは共有されるのかされないのか。
    - [[🤔httpだとクリップボードが使えない？#606da96aaff09e0000d54778]]
    - [[🤔選択肢回答だけを受け付ける]]
    - [[🤔モードの変更をメニューにつける？]]

[[pKeicho202103-202104done]]

Memo
- [[終わりのデザイン]]
    - 派生で「[[質問がコマンドボタンを作れるようにする]]」
    - [[会話ログ2021-01-30]]
        - これの終盤はおそらく、キーワードが多くて十分発展したとみなしてシンボル間の関係を聞くモードに遷移した後、スコアの高い単語を使い果たしてるのに関係を聞くモードのままなのだと思う
        - おそらくキーワードスコアの分布からそれを判断して、
        - ・終わりを提案する
        - ・新規チャットを提案する
        - ・探索モードに戻る
        - のいずれかをするのが適切だと思う。
- [[質問自然度データセット]]
    - 特徴量をもっと改善すべき
    - 関連: [[二つの引数をとる質問のチューニング]]
        - 対称な質問を繰り返さない: done
        - 2つの引数をとる質問についても自然さの収集が必要
    - 関連: [[会話中に良し悪しフィードバック]]
        - NGフィードバックを学習データにする
        - →データ量が足りないし、学習データとしての質が低い
            - 能動学習で僕が教える方が良さそう
- ---
- [[Regroupへワンクリックでインポート]]
- [[対象として不適切なものを分析対象から除外するignoreファイル]]
    - (まともに使われてないログなど)
- [[フィードバックボタン:いいね]]
- 注目すべき対象を表現するためにスコアをいじってはいけない
    - これが原因で「ユーザの発言の中に実際に繰り返し出てきたこと」と「システムが注目すべきと判断していること」の混同が起きている
    - [[スコア=発展度, not注目度]]
- [[聞き出しチャットシステムのタスク整理版を作るとしたら]]
- 「つ、つよい」という入力に対して
    - 「つよい」が形容詞なのでキーワードとして選ばれない
        - "その「つよい」はどんな種類の「つよい」ですか？"はアリな質問だから抽出した方が良いのでは
    - 「つ」が名詞にもなりうるためキーワードに含まれてしまう
    - 結果「つ」に掘り下げ質問をしてしまう
- よくないキーワードを弾く
    - CUI版にはあった
    - Mattermost版にする時にオフにしてそのまま
    - NGKWフィードバックを使って学習しよう
    - →いいキーワードなのにユーザが気づかずにNGKWしてるケースが結構多い、ユーザから学ぶとバカになる
        - 明らかにダメなものだけリストに入れる形にした
- フィードバックしたいこと
    - キーワードの抽出がそもそもNG
        - > 微妙に買えてきたなw
        - > そのwは、どこにありますか？
        - NGKWコマンドで。
    - 入力に対して選んだキーワードがNG
        - 例:
            - [[真昼の太陽]]
        - キーワードの抽出は問題ないが、ユーザが掘り下げてほしい方向性と違う
            - これは事前の学習でどうこうならないかもなので、「いや、そっちじゃなくて」って言えるといいね
            - NGKWコマンドとUPKWコマンドって形で実現された
    - 選んだキーワードと質問の組み合わせが良くない
        - NGフィードバックを学習データにする
- [[シンボルの関係が同一]]
    - > 2つのシンボルの関係が同一だと回答されたらシンボル間の関係の質問をするのはイマイチ
    - 「同じ」というボタンが出現して、それを押したらコマンドとして二つのキーワードのマージが行われたら良いのでは
        - キーワードの片方が消えることで何かバグが起こりそうだからちゃんとテストする
- 状態遷移の仕組み
    - 状態遷移図はどうやってメンテされるべきか
    - どうやって柔らかくするか
    - 状態に対する信念
        - [[部分観測マルコフ決定過程]]
    - [[会話ログ:状態遷移について]]
        - そもそも単語ごとに持っているスコアが1次元なのは良くないのでは？という話
            - [[スコア=発展度, not注目度]]
    - [[キーワードと質問の選択は内積注意]]
    - 比較的少数のパラメータで記述される
        - MUSTの制約を守りつつ、BETTERの指標をなるべく良くしたい
        - パラメータ探索
        - 質問選択肢の選択バリエーションが多い(すべて1回以上でること)も制約
- [[基本5質問の出現順番]]
- 累積スコア計算に減衰を入れる？
    - 減衰を入れた方が良いのでは？と思ったこともある
    - 一方で、最初の「この対話で何が起きると良いのか」にしっかり回答してる場合、そこのキーワードを時々思い出させた方が良いかもという気もする
        - これに関しては最初の回答が雑なケースもしばしば観測される
        - 話してるうちにだんだん整理されて、自分が何を求めてたのか明らかになる、ってのはよくあることだから、最初の発言を重視しすぎるのもな…
- [[write_learning_pair]]
    - ユーザの長い入力を引き起こす質問が良い質問という仮説
- [[キーワードを取らない質問はenvから特徴量を取るべき]]
- [[キーワードが分割されてしまった場合のリカバリ手段がない]]
- [[気づきの判定]]
- [[序盤のデザイン]]
    - 初手でキーワードの含まれない発話をしてる人がいる。今はエラーにならないようにキーワードのない質問をとりあえずしてるけど、そもそも使い方を理解してなさそうなのでヘルプに誘導した方が良いかも
        - 「キーワードを掘り下げる」を理解してないケースと、プログラムをいじめたいケースとがある
        - [[プログラムの側から会話打ち切り]]できてもいいかも
    - キーワードが発展する前にNGKWで削りすぎると、「泉が枯れた」ような状態になる
        - たぶんNGKWを使いすぎてキーワードが枯渇し、プログラムが直近の発言から出たキーワードに飛びついて質問し、それが本題からずれてるからまたNGKWされ、という悪循環にハマっている。
        - うまくキーワードがいっぱいでて賑わってる状態に誘導していくにはどうすればいいのか
        - 各フェーズで達成すべき値がどこまで達成されてるかをパーセント表示する？
        - キーワードが少なすぎることやNGKWのペースが早すぎることを指摘する？
            - キーワードが少ない時には少し待たないとボタンが押せないようにすれば良いのでは
            - [[いいよどみ]]
- 質問が回答の一部を指定できるといい
    - 「同じですか？違いますか？」は「同じ」ボタンを表示する
        - 選ぶとキーワードのマージコマンドとして機能する
    - 「ここは終わるのに良いところですか？」は「はい」「いいえ」の二択にする
        - その選択が直接学習データに使える
- [[ppoi]]
    - 読み返してアップデート
- キーワード抽出にRAKE的要素をつける
    - 自分の過去発言/過去ログ/Scrapboxに出現する並びを長めに抽出



- [[pKeicho-done-2021-02-05]]


---
[[Keichobot History]]

> これは「既にあなたの中にあるけども言語化できていないもの」を言語化して取り出すことを支援するソフトウェアであり、あなたの相談に対して答えを与えるソフトウェアではありません。


キーワード: [[チャットボット]] <img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/>

[[キーユースケース]]

[[pKeicho単語頻度]] / [[ソースコードの単語頻度]]

-----
[[書き出しツールから呼び出す？]]
[[ローカル環境に移動？]]
-----

- [[pKeicho-Mattermost-done]]


[[Keicho-Mattermostの状態遷移]]
[[Keicho-CUI: kw type]]
[[(2019/6)Keicho学習]]
- 相槌に関してだけキーワードを取る個数が不定(0 or 1)
    - 2つの質問に分割すべきかも

[[pKeicho-done]]
入力行とキーワード抽出結果のペアが必要では？→done


