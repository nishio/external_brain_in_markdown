---
title: "if文から機械学習への道"
---

![image](https://gyazo.com/e6afaa643e5d90b03e2983764d9aa62b/thumb/1000)
if文から[[機械学習]]への道 2017-09-26 BPStudy#121
サイボウズラボ/ BeProud技術顧問理学博士/技術経営学修士
西尾泰和
ver.2 2017-09-29公開
ver.3 2018-06-22図の清書
ver.4 2023-06-10OCR結果の清書と加筆

![image](https://gyazo.com/678badbaf3519afe5324b43b56057ea7/thumb/1000)

機械学習って今書いてるプログラムから遠い世界だと思ってませんか?

![image](https://gyazo.com/2ac79c15ccd864452d5dc1da9b655b3a/thumb/1000)
このスライドの目的
- みんなのよく知っているif文と機械学習の橋渡しをすることで地続きにし、実務で機械学習を使えるようにする。
- また、機械学習のビジネス導入の進め方を4ステップに分けて一歩一歩解説する。

![image](https://gyazo.com/2608d362e16adbca7400a3553c1a0e11/thumb/1000)
if文4 if(`条件`){ …}

![image](https://gyazo.com/d3497b5db2fd5e7844aaf3bf4c9b6457/thumb/1000)
if文の仕組み
- 条件がTrueの時に、中身を実行

![image](https://gyazo.com/0cef01d7cf9bcf217e4214d21c3a8bbb/thumb/1000)
条件が複数ある時
- 条件x1と条件x2のどちらかがTrueの時に実行したいなら、どうする?

![image](https://gyazo.com/b4431e9b8bb3903f3d2fdc759cd7b41e/thumb/1000)
or
- `if(x1 or x2){ …}`

![image](https://gyazo.com/69bd44856d9f2285220fc323508164de/thumb/1000)
条件が複数ある時
- 条件x1と条件x2の両方がTrueの時に実行したいなら、どうする?

![image](https://gyazo.com/d72be5377d0a3983ccbfdcd350d14151/thumb/1000)
and
- `if(x1 and x2){ …}`

![image](https://gyazo.com/03d5a280e95da798cdadfe8e2b07fc78/thumb/1000)
条件が複数ある時
- 条件x1, x2, x3の内、2つ以上がTrueの時に実行したいなら、どうする?

![image](https://gyazo.com/facfe680f16b01fcebcda515f5cf3177/thumb/1000)
複雑!
- `if((x1 and x2) or (x1 and x3) or (x2 and x3)){ …}`

![image](https://gyazo.com/1846ba35a0e14355e161b4868a882f93/thumb/1000)
条件が複数ある時
- 条件x1, x2, …, x5の内、3つ以上がTrueの時に実行したいなら、どうする?

![image](https://gyazo.com/ba6368d2da9a70acd23c06e5fe46f8d3/thumb/1000)
複雑!
- `if((x1 and x2 and x3) or (x1 and x2 and x4) or (x1 and x2 and x5) or…){ …}`

![image](https://gyazo.com/dd99a61bf5d2979a309b7ea1ff6b6519/thumb/1000)
もっと良い方法がある!

![image](https://gyazo.com/cc5c2293acc809279378d9a7bb286701/thumb/1000)
[[真偽値を数値にする]]
- Trueを1、Falseを0に変換すると「3つ以上がTrue」は「足したら3以上」に変わる。
- `if((x1 + x2 + x3 + x4 + x5) >= 3){ …}`

![image](https://gyazo.com/e6c32404c0b84b44e4174b40a44a3cdd/thumb/1000)
andもorも同じ形にできる
- `x1 and x2 and x3 and x4 and x5` =条件x1, x2, …, x5の、すべてがTrue =足したら5以上
- `x1 or x2 or x3 or x4 or x5` =条件x1, x2, …, x5の、どれかがTrue =足したら1以上

![image](https://gyazo.com/5fa7ff716d1dcd1460df8b8b9be293b4/thumb/1000)
andもorも同じ形にできる
- 条件x1, x2, …, x5の、すべてがTrue
    - `(x1 + x2 + x3 + x4 + x5) >= 5`
- 条件x1, x2, …, x5のうち3つ以上True
    - `(x1 + x2 + x3 + x4 + x5) >= 3`
- 条件x1, x2, …, x5の、どれかがTrue
    - `(x1 + x2 + x3 + x4 + x5) >= 1`

![image](https://gyazo.com/076f4e8c6975883a642d2b39c2dcf49c/thumb/1000)
右辺をそろえてみる
- 条件x1, x2, …, x5の、すべてがTrue(弱い)
    - (1/5 *x1 + …) >= 1
- 条件x1, x2, …, x5のうち3つ以上True
    - (1/3 *x1 + …) >= 1
- 条件x1, x2, …, x5の、どれかがTrue(強い)
    - (1 *x1 + …) >= 1


![image](https://gyazo.com/6e770115e61dfbc3f13e458737536689/thumb/1000)
強さ=重み
- 条件の「強さ」のようなものが係数([[重み]])の大きさで表現される。

![image](https://gyazo.com/ffe9c0ca59d9a378ff8130d3ea02438d/thumb/1000)
問
- 条件x1, x2, …, x5の、すべてがTrueまたは条件x6, x7, …, x10のうち3つ以上Trueまたは条件x11, x12, …, x15の、どれかがTrueを表現するにはどうすればよい?

![image](https://gyazo.com/b8b54921f347a17194d4770aa6bbab08/thumb/1000)
重みは条件ごとに異なってもよい
- 1 *x1 + ... + 1/3 * x6 + … + 1 * x11 >= 1

![image](https://gyazo.com/c7609fc432680f2e0b30fee3cdcc137c/thumb/1000)
重み付き和の方法
- 真偽値のTrueを1、Falseを0にし、条件の強さを重みにして掛け合わせ、足し合わせる
- これによってandやorの組み合わせでは苦労するような複雑な条件を記述することができる。
- 否定が負の重みで実現できることと、xorが表現できないことは割愛

![image](https://gyazo.com/a85146d3aef08470c3995de225807c06/thumb/1000)
重みはどうやって調整する?
- 1:今やったみたいに人間が決める
- 2:大量のデータを元に機械が決める=機械学習

![image](https://gyazo.com/7822bfdf9a569437e4bf141d1c507d74/thumb/1000)
具体的なコード
- 今回の内容は[[ロジスティック回帰]]を使って学習できる。
- `from sklearn.linear_model import LogisticRegression`ってやって`fit(X, y)`を呼べば重みが自動調整されて`predict(X)`を呼べば重み付き和を計算して判断してくれる。楽ちん。
- ロジスティック回帰についてくわしく知りたい人は、サイボウズラボの中谷秀洋さんが技術評論社のサイトで連載しているのがおススメ
    - [第18回 ロジスティック回帰 | gihyo.jp](http://gihyo.jp/dev/serial/01/machine-learning/0018)

![image](https://gyazo.com/22948174b3cdeeaa2007aa9b55241329/thumb/1000)
まとめ
- 複雑な条件はand/orで書くのが大変。
- 重み付き和で置きかえると楽になる。
- 重みはデータが十分あれば機械学習で決められる。
- 今回説明した程度のことはscikit-learnを使えば数行でできる。

![image](https://gyazo.com/b0dbff4c39165e40f944e07856a96f54/thumb/1000)
ここまで機械学習の技術
ここから機械学習のビジネス4つのステップ

![image](https://gyazo.com/b365eee5095d50b7bc6b50e95e7b6ddf/thumb/1000)
アカデミアとビジネスの違い
- [[アカデミア]]
    - データが公開されている
    - 枯れた技術はとっくの昔に調査済み
    - 新しい手法を考案して精度を競い合う
- ビジネス
    - データが公開されてない
    - (枯れた技術を使う)

![image](https://gyazo.com/1ffa3b1f2dd43389bfa758fee341e4a5/thumb/1000)

ビジネスの目的
- [[顧客価値]]
- ([[新規性]]ではない)

![image](https://gyazo.com/90a2986632d1803becd10903cfdc80dc/thumb/1000)
顧客価値を体感するための小問
- ある宝石の原石は、割ると1/2の確率で宝石が入っていて2万円で売れる。
- 原石は1つ9500円で買える。原石は硬いので1日に20個しか割れない
- Q1: 1日に稼げる収益の期待値はいくらか

![image](https://gyazo.com/a4119bf74ac65c2c56dd3cae6d388e37/thumb/1000)
A1収益の期待値
- A1: 1/2の確率で20000円手に入るので、1個あたりの収入の期待値は10000円。
- 1個あたりの仕入れ価格は9500なので、1個あたりの収益は500円。
- 1日に20個処理できるので、1日あたりの収益は10000円。

![image](https://gyazo.com/e9bccade278d7111b91fabc3c685bffb/thumb/1000)
Q2 加工速度二倍の装置
- Q2:原石を人間の2倍の速度で割る機械を手に入れたとする。
- つまり、1日に割ることができる原石の数が20個から40個に増えたとする。
- 収益の期待値はいくら増えるか?

![image](https://gyazo.com/c4414907eb24a8144a0b0c0b46d0f209/thumb/1000)
A2 加工速度二倍の装置
- A2:原石1個あたり500円の利益なのは変わらない。
- 1日に処理できる量が20個から40個に増える。
- 20個増えるので、利益は1万円増える。

![image](https://gyazo.com/78a99b9fd5288a6f023048d38e2b20b6/thumb/1000)
Q3 60%の識別器
- Q3: 60%の確率で宝石の入った原石を当てる識別器*が買えるとする。
    - *原石を買う前に使うことで「60%の確率で宝石が入っている原石」を9500円で手に入れられるようになるとします。
    - お店の人が嫌がりそう、という点は今回は気にません。
    - またQ2の機械は手に入っておらず、1日に割れる数は20個のままとします。
- 収益の期待値はいくら増えるか?

![image](https://gyazo.com/deda9a9fc5b9e4a00ca891953de2531a/thumb/1000)
A3: 60%の識別器
- 60%の確率で20000円手に入るので、1個あたりの収入の期待値は12000円。
- 1個あたりの仕入れ価格は9500円なので、1個あたりの収益は2500円。
- 1日に20個処理できるので1日あたりの収益は5万円。
- 4万円増える。

![image](https://gyazo.com/c2367038f172aeedf2c7fbe5876dff31/thumb/1000)
つまりこの問題設定では
- 「加工速度を2倍にする装置」は顧客の利益を1万円増やし、
- 「精度60%の識別器」は顧客の利益を4万円増やす。

![image](https://gyazo.com/524a8c04a98e2b004da22e17cbc7e68f/thumb/1000)
教訓
- この問題設定では「精度60%の識別器」が「加工速度を2倍にする装置」の4倍の顧客価値を持っている。
- どの程度の精度でどの程度の顧客価値を生み出すことができるかは[[ビジネス要件]]によって決まる。
- 精度は必ずしも重要ではない

![image](https://gyazo.com/c7d047af5c2e3730b304e38971a8332d/thumb/1000)
ビジネス要件
- 精度を高めようと考える前に、まず[[顧客が何を求めているか]]、どういう[[制約条件]]があるのかを明確化する必要がある。
- 最新の論文に書かれた手法を実装しても、その手法が要求する量のデータを顧客が用意できないのであれば、その実装は顧客価値を持たない。

![image](https://gyazo.com/247dc788120a5b347094b8c0f2178cc3/thumb/1000)
顧客は専門家ではない
- 多くの場合顧客は機械学習の専門家ではないので、必要な精度も、満たすべき制約条件も、明確に言語化することができない。
- なので、これを高速に学び取ることが必要。

![image](https://gyazo.com/a3444a0672815f849793029a4690c5d8/thumb/1000)
[[Minimum Viable Product]]
- ITベンチャー経営の方法論「リーン・スタートアップ」で提唱された考え方。
- ベンチャーは資金に限りがあるので素早く顧客ニーズを理解しなければならない。
- そこで、最小限のコストで雑な製品を作り、それを実際に顧客に見せてみることで、顧客のニーズがどこにあるのかを探る。

![image](https://gyazo.com/266ac1da93352348751aa9fb9b32696e/thumb/1000)
最小限の実装=実装しない
- 「[[コンシェルジュ型MVP]]」と呼ばれる

![image](https://gyazo.com/83a5de9e5964bc206493fbaf97cd3c0d/thumb/1000)
ステップ1
- 人間がやると想定して次の質問に答えよう
    - ①[[顧客価値]]: 顧客は何がどうなると嬉しいのか
    - ②[[人がやる方法]]: それを人間がやるならどうやってやるか(既にやっている人間がいるのか?いないのか?)

![image](https://gyazo.com/89af264374c78c751c8eac8a1e9b1d0a/thumb/1000)
(2)人間がどうやってやるか
- 既にやっている人がいる、または、やり方はわかる。
- しかし時間や労力が掛かりすぎる。
- →チャンス!機械化で時間や労力を減らすことが顧客価値になる!

![image](https://gyazo.com/5d9d44baa4a45d32876c3e95ab502108/thumb/1000)
(2)人間がどうやってやるか
- 顧客側などでやっている人がいる、しかし、自分はやり方がわからない。
- →何か重要な情報の伝達漏れが発生している。

![image](https://gyazo.com/80a28a46c291fb43ac63e53b014b79ba/thumb/1000)
(2)人間がどうやってやるか
- 人間がやる方法を、顧客も自分もわからない
- →そもそも無茶なことを妄想している可能性。

![image](https://gyazo.com/0721a06be0dcec2cad1638dbdd15c829/thumb/1000)
例:スパムフィルタ
- Q1 顧客は何がどうなると嬉しいのか
- A1 顧客はメールボックスにスパムメールがたくさんあって困っている、スパムがなくなるとうれしい
- Q2 それを人間がやるならどうやってやるか
- A2 メールの本文を見て、スパムかどうか判定して、スパムは別のフォルダに移動する

![image](https://gyazo.com/6d2a0c22cc8ddba81b87c7ef26856136/thumb/1000)
ステップ2
- 人間を箱に入れる。
    - この箱には電子データしか出し入れできない。
    - (リモートワークと考えてもよい)

![image](https://gyazo.com/dbb77c9716d7122a81cedfdc731007c6/thumb/1000)
ステップ2
- ③入力データ: 人間が(2)をするために、箱にどんなデータを入れるのか?
- ④出力データ: 人間が(2)をすることで、箱からどんな出力データが出てくるのか?

![image](https://gyazo.com/96f424014443c9cb4a7318179989d194/thumb/1000)
ステップ2
- ⑤得る方法: 入力データ(3)はどうやって入手するのか? (最初の一歩と継続的にやる方法)
- ⑥与える方法: 出力データ(4)をどうやって顧客価値(1)につなげるのか?

![image](https://gyazo.com/8c650af8930351e96206a114682cdef8/thumb/1000)
この4つの質問の答える順番は問わない。
- 例1:顧客に〜をするために(6)、〜を出力する(4)、そのため入力〜を入れる(3)、これをどうやって入手しようか?(5)
- 例2:今データが入手できている(5, 3)ここから顧客価値を生むにはどうするか?(6)そのためにはどういう出力が必要か?(4)

![image](https://gyazo.com/b25029ef607e5f77be73b1df99a3e705/thumb/1000)
例:スパムフィルタ
- Q2それを人間がやるならどうやってやるか
- A2人間がやるなら、メールの本文を見て、スパムかどうか判定して、スパムは別のフォルダに移動する
- Q3人間が(2)するために、どんなデータを入れる必要があるか?
- A3メールの本文の情報が必要。タイトルや送信者も貰えるなら貰いたい

![image](https://gyazo.com/7310d7584a70d6033a375a7d94a9ebd6/thumb/1000)
例:スパムフィルタ
- Q4人間が(2)をすることで、箱からどんな出力データが出てくるのか?
- A4各メールに対して「スパムである、スパムでない」のラベルを出力

![image](https://gyazo.com/f25c1b978c867c1806b8042137537af7/thumb/1000)
例:スパムフィルタ
- Q5 入力データ(3)はどうやって入手するのか?
- A5 最初の一歩としてはとりあえずメールをエクスポートしてもらえれば。
    - 継続的にやるにはメーラからデータを取る方法を作るか、メールサーバの側に手を加えるかが必要そう。
- 追記: 最初の一歩のデータをもらって実験をすることと、メールサーバに手を加えて継続的にデータが得られるようにすることのどちらの優先度が高いか
    - 基本的には「機械学習で識別できるかどうか」は不確実性が高いので早く検証するのが良い
    - 状況によるのでどちらから先にやるか、それとも並列にやるのか、ケースバイケースで判断する必要がある


![image](https://gyazo.com/0879baad881c2caefbb9052277b1d2d4/thumb/1000)
例:スパムフィルタ
- Q6出力データ(4)をどうやって顧客価値(1)につなげるのか?
- A6スパムである/ないのラベルを見て、メールを振り分けする
- 追記: 「顧客価値」につながるためには「メールを振り分ける」が必要だ、と言語化されたら、次は「その振り分けはどのようにすれば可能なのか？」と掘り下げていける
    - メールを表示するプログラムの側に手を加えることができるのか？
    - 例えばスパムと判定されたことを示す特定の文字列をヘッダに入れて、ユーザに振り分けの設定をやってもらうか？

![image](https://gyazo.com/31c5a1dc3b9c17e5c05d247fed8d8b50/thumb/1000)
アルバイト
- (7)箱の中の人が、まったく知識のないアルバイトだとしたら、どんなマニュアルを用意する必要があるか?これを考えておくと次のステップが楽になる。

![image](https://gyazo.com/06f41fcadaf35bf4c7dcd2209adeb929/thumb/1000)
ステップ3
- ステップ1:人間がやる
- ステップ2:箱の中の人間がやる
- ステップ3:箱の中の機械がやる
- 箱の中の人をコンピュータに置き換える。

![image](https://gyazo.com/81315673a08b3471604deb5efd160bf5/thumb/1000)
最初のプログラム
- (8)箱の中のコンピュータが(2)をするためのプログラムを書く
- 完璧である必要はない
- 高度なアルゴリズムである必要はない
- 精度は低くてよい
- 「とりあえず動く」ぐらいでよい

![image](https://gyazo.com/87559a341c14e9388f085dce931723b5/thumb/1000)
実行してみて顧客に見せる
- (9)プログラム(8)に実際にデータを入れて振る舞いを観察する。(精度はどう?速度は?)
- (10)顧客はこれで満足する?

![image](https://gyazo.com/e99aeb165521a181c983c563af3e9735/thumb/1000)
顧客に見せるのが怖い?
- 精度が出ていないのに顧客に見せるのは怖い?
- しかし顧客が何を重視するかは顧客にしかわからない。
- 低品質だと顧客に言われたとしても、それは顧客が何を重視するかを知るチャンスになる。see「[[リーン・スタートアップ]]」

![image](https://gyazo.com/b39ca81e84965aadc16736a92a5892aa/thumb/1000)
顧客が満足しないなら
- (11)どう満足しないのか[[具体的不満]]を収集する
    - (どういう入力の時にはどういう出力が出てほしいのか?これを[[教師データ]]という)

![image](https://gyazo.com/b1a9434f253aba06f7d81479b3ee77ee/thumb/1000)
ステップ4
- ようやく機械学習!

![image](https://gyazo.com/f18fe3a70c5957694e082f39347edbe5/thumb/1000)
科学的方法論
- 教師データが充実すると、アルゴリズムの良し悪しが定量的に測れるようになる。
    - (教師データの一部を検証用のデータに使う)
- 機械学習にしたからと言ってよくなるとは限らないのでプログラム(8)とキチンと比較する。
- 仮説・実験・検証・修正のサイクルを回す。
    - ([[PDCAサイクル]]/[[科学的方法論]])
    - サイクルを回して[[改善]]していく。

![image](https://gyazo.com/8ad67b18a62bf39ad90f4fb10b16dc6f/thumb/1000)
改善の具体的方法
- 「現時点のアルゴリズムが正しく分類できてないデータ」を抽出して眺め、それらを正しく分類するためにはどうすれば良いかを考える。(特徴量の追加など)
- ロジスティック回帰などの「判断の自信」を返してくれるアルゴリズムなら、「自信のない結果」を見て教師データの追加を行う。([[能動学習]])

![image](https://gyazo.com/09ad0d2020987f7ccfdb6e7e5159f610/thumb/1000)
間違えないように何度も言う
- ビジネス上重要なのは顧客価値。精度ではない。
- 例え精度が99%でも、間違う1%が顧客にとって致命的なら、精度60%でその間違いをしないプログラムの方が顧客価値が高い。

![image](https://gyazo.com/434afc8e9a3fa8b193bb1d9e920cb3ff/thumb/1000)
まとめ
- ビジネスでは顧客価値が重要
- 顧客もあなたも何が顧客価値か正確に理解していない
- 素早く理解するために最小限の工数で実験を繰り返す(Minimum Viable Prodict)
- 実験によって不満点や顧客価値が徐々に具体化されていく
- 改善を繰り返して顧客価値を増やしていく

![image](https://gyazo.com/b8723e89dee56ac0ffbcdbb63c5b175c/thumb/1000)
以下補足と質問・回答

![image](https://gyazo.com/53c4188fa0b246a64536737c483e1619/thumb/1000)
補足
- これは「顧客の要求が明瞭でない、仕様書がない状態でのソフトウェア開発」に似ている。
- 違う点は、顧客が不満な場合に「ソフトウェアを作り直す」ではなく「学習データにその情報を追加」で解決できる可能性があるところ。
- とはいえ常にデータで解決できるわけではないので、やはり最小限の実装で実験するのは大事。

![image](https://gyazo.com/1e2782fc81f6f34cb3a7c345987624d6/thumb/1000)
補足:バッドパターン
- ①手軽な方法
- ②テキトーなデータ
- ③スゴイ機械学習
    - ココで時間を使いきる
- ④精度高い出力データ
- ⑤雑にぶつける
- ⑥ミスマッチ: 顧客「コレじゃない」
- ⑦ゆきばのない不満
これを避けるためにも実験を繰り返せる形にすることが大事

![image](https://gyazo.com/028b6f361f287e5f4c71128096950f91/thumb/1000)
Q&Aマニュアル書き
- (7)と(8)についての質問: “アルバイトのためのマニュアルが書けるならプログラムも書けるはずでは"
- はい。「アルバイトのためのマニュアルが書けないぐらい仕様が曖昧だったらプログラムを書くのは無理だよね」が言いたいことでした。
- 「マニュアルをどう書くか?」を考えることでまだ言語化されていないものに気付き、言語化が促されるのです。(次ページに具体例)

![image](https://gyazo.com/85cff9c46f65d0cd51d5d907b15e3894/thumb/1000)
- 例:スパムフィルタ
- 実現したいこと: >(2)“メールの本文を見て、スパムかどうか判定し、スパムは別のフォルダに移動する"
- あなた「本文を見てスパムかどうか判断して」
- バイト「どうやって判断するんですか?」
- あなた「例えば○○って単語が入ってたらスパム」
- 気付き: 最初の一歩のプログラム(8)を「NGキーワードが含まれてるか判定」にしたらよい
    - 補足の補足:アルバイト向けマニュアルの作成は「最初のプアなプログラム」を書く上での助けになることが目的なので、さらさらプログラムを書けるなら飛ばしてもよい。

![image](https://gyazo.com/4a3dfee51ecfe07b6d88a301aea93aee/thumb/1000)
工数
- Q: どれくらいの工数がかかると思えばいいか?
- A: ケースバイケース。
    - 例えば枯れた技術、ロジスティック回帰にデータを入れてみて、サクッと精度が出て顧客から一発OKもらえることもあるし、逆にぜんぜんダメということもある。「実験」するしかない。
    - 工数を見積もることは困難なので、決まった時間で成果を確約するような契約を結ぶのは危険。

![image](https://gyazo.com/fc41f62b85bfe9cc2307f72bbfc8a771/thumb/1000)
精度
- Q:顧客に精度保証を求められたら
- A:「どのくらいの精度になるかは実験してみないとわからない」ということを顧客との共通認識にしていく必要がある。
- 精度を確約するのではなく「良いものができるかもしれない試行錯誤」に対してお支払いを頂く形の契約が良い。
- なるべく小さい単位で実験をして顧客とのコミュニケーションを密にしていく必要がある。

![image](https://gyazo.com/080326429c6036788508564f241ef605/thumb/1000)
- 判断のコストと精度
- 知識のある「専門家」が判断
- 知識のない「アルバイト」が判断
- 機械が判断
- 判断の精度もコストも上が高い
- 機械は24時間働かせても疲れないし労基署に怒られることもない。
- 精度は必ずしも高くない*が、コストの低下でビジネス上の価値が生まれる。(*頑張り次第)
- 2023年追記: GPT-3.5が広いタスクに対して人間を超えた
    - [[ChatGPT Outperforms Crowd-Workers for Text-Annotation Tasks]]
    - つまり「機械」が「知識のないアルバイト」と比べて精度が高くなったわけだ
    - 「クラウドソーシングで知識もやる気もない素人の人間に教師データを作らせるよりGPT-3.5を使った方がよい」という時代になった

![image](https://gyazo.com/129dbf5d9009c5acb00cf6e9e5222364/thumb/1000)
Deep Learning
- Q: “人間が条件を明確化できてなくてもDeep Learningなら自動でできるのでは?"
- A:半分正しい。
- 画像処理の分野では、例えば100x100のモノクロ画像でも「入力の値が10000個ある」という辛い状態になる。こういう入力をうまく扱おうと専門家が何十年もの間、色々な条件を考案してきた。
- 畳みこみを繰り返す特殊な形のニューラルネットを作って、大量のデータで学習してみたら、意外なことに専門家が工夫して実装したものより良い精度が出た。
- これが正しい半分。正しくない半分は次のページ。

![image](https://gyazo.com/6f6bcd421095ca0da5132434ecc692d1/thumb/1000)
Deep Learning
- この成功によりDeep Leaningに注目が集まり文脈を抜かして「Deep Learningを使うと人間より精度の高い判断をするプログラムが作れる」と伝言ゲームがゆがむ。
- その結果、全然違う条件の問題に対して「これもDeep Learningでなんとかなるのでは」と考える人が増えた。
- 問題条件が変われば手法の有効性も変わるので、基本は「枯れた手法から順に小さい実験を繰り返す」しかない。

![image](https://gyazo.com/122c20f164c55c426df1f25b89a881dd/thumb/1000)
能動学習
- Q:[[ナイーブベイズ]]よりもロジスティック回帰で能動学習した方がいいか?
- A:ナイーブベイズもロジスティック回帰同様に信頼度を出せる手法なので、ナイーブベイズで能動学習したらいい。
- 補足:今回は割愛したけども、ロジスティック回帰もナイーブベイズも「[[確率モデル]]」であって、「この入力がクラス1になる確率は0.8だな」みたいな出力を出すモデルです。これをこの発表では「[[判断の自信]]」って表現していました。

![image](https://gyazo.com/4a3ee64749819d105511033f7af924f1/thumb/1000)
微分
- Twitterの感想「行列も微分も出てこない」
- 機械が重みを調整する時に「正解とのずれが小さくなる方向に重みをちょっと変更しよう」ってやる
- これを数学語で言うと「『正解とのずれ』を重みで微分して勾配を求め、勾配方向に重みをちょっと変更しよう」になるわけです。

![image](https://gyazo.com/866db9f8c322d2d08ee39ee3d403825d/thumb/1000)
行列
- ロジスティック回帰では、例えば条件が15個あったら「重み」という値が15個できる。
- これを数学語で言うと「ベクトル」になる。
- ニューラルネットはロジスティック回帰的なものが複数個集まってるので、仮に10個集まってるとしたら15x10個の値ができる。
- これを数学語で言えば「行列」になる。

![image](https://gyazo.com/010ed83b713d9319fc3c8d5a32cf187b/thumb/1000)
あいまいな判断
- 「P21は、例えばx1,x2,x3,x4,x6がTrueだと17/15になり、Trueになる。数学的には正しくない」
- そう、そこが重要なところ(強調し忘れました)
    - 元の式と、重み付き和の式は等価ではない。
- しかし機械学習を使おうという時「どういう条件式なら顧客価値が生み出されるか」がそもそもわかっていない。
    - なので「元式と等価であること」には顧客価値がない。
- 論理的にきちんと記述することを手放して、雑であいまいな条件式で表現し、それがちゃんと機能するかどうかは、論理ではなく実データでのテストで担保する。これが機械学習の基本的スタンス。

![image](https://gyazo.com/a694f0b35ecfdec0b7641b1086001d3c/thumb/1000)
補足(宣伝)
- 「データを観察することが大事」と明記・強調することを忘れていました。
- 僕が監修したPyQの「はじめての機械学習」ではデータを観察してif文を作るところからロジスティック回帰までを小さいステップで一歩一歩解説しています
- 機械学習の基本をif文から学ぼう
- しきい値を見つけよう
- 可視化してしきい値を見つける
- しきい値が決められないデータの扱い方
- 2次元のデータから分類
- 2次元データをプロット
- 1次方程式を用いた分類
- はじめての機械学習:ロジスティック回帰
