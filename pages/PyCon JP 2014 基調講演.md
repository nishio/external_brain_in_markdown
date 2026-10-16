---
title: "PyCon JP 2014 基調講演"
---

- 2014-09-17
    - [PyCon JP Blog: PyCon JP 2014 のキーノート（基調講演）スピーカーが決定しました](http://pyconjp.blogspot.jp/2014/06/pycon-jp-2014.html)
    - [PyCon JP 2014 in Tokyo | September 12th – September 15th](https://pycon.jp/2014/)
- 資料
    - [日本語版](http://www.slideshare.net/nishio/pyconjp-keynote-speach-japanese-version)
    - [英語版](http://www.slideshare.net/nishio/pyconjp-keynote-speech-english-version)

-----
![image](https://scrapbox.io/files/6ad18cdc6bd7d205ec7ea8a8.png)
Rediscover with Pythonサイボウズ・ラボ西尾泰和質疑応答加筆バージョン2014-09-17 14年9月17日水曜日1

![image](https://scrapbox.io/files/6ad18cdd6bd7d205ec7ea8cb.png)
evil pythonista 14年9月17日水曜日2

![image](https://scrapbox.io/files/6ad18cde6bd7d205ec7ea8f3.png)
evil pythonista 14年9月17日水曜日3

![image](https://scrapbox.io/files/6ad18cdf6bd7d205ec7ea915.png)
evil pythonista •2006年LL Ring「じゃんけん2.0」14年9月17日水曜日3

![image](https://scrapbox.io/files/6ad18cdf6bd7d205ec7ea933.png)
evil pythonista •2006年LL Ring「じゃんけん2.0」•いろいろな言語のプログラマが各言語でプログラムを書き、通信対戦でじゃんけんする14年9月17日水曜日3

![image](https://scrapbox.io/files/6ad18ce06bd7d205ec7ea95a.png)
evil pythonista •2006年LL Ring「じゃんけん2.0」•いろいろな言語のプログラマが各言語でプログラムを書き、通信対戦でじゃんけんする•この程度のプログラムなら1行で書ける! 14年9月17日水曜日3

![image](https://scrapbox.io/files/6ad18ce16bd7d205ec7ea986.png)
改行のある構文は使えない•if •while •try..except 14年9月17日水曜日4

![image](https://scrapbox.io/files/6ad18ce26bd7d205ec7ea9b0.png)
How to? 14年9月17日水曜日5

![image](https://scrapbox.io/files/6ad18ce36bd7d205ec7ea9e5.png)
How to? •if →and/orの短絡評価を使う14年9月17日水曜日5

![image](https://scrapbox.io/files/6ad18ce46bd7d205ec7eaa06.png)
How to? •if →and/orの短絡評価を使う•while →無限にyieldする便利ライブラリfrom itertools import count 14年9月17日水曜日5

![image](https://scrapbox.io/files/6ad18ce46bd7d205ec7eaa26.png)
How to? •if →and/orの短絡評価を使う•while →無限にyieldする便利ライブラリfrom itertools import count •try..except →“例外を投げて死ぬ可能性のある処理"を子プロセスとして起動し、終了時のエラー出力を読む14年9月17日水曜日5

![image](https://scrapbox.io/files/6ad18ce56bd7d205ec7eaa4a.png)
14年9月17日水曜日6 [http://www.nishiohirokazu.org/blog/2006/08/python_12.html](http://www.nishiohirokazu.org/blog/2006/08/python_12.html)

![image](https://scrapbox.io/files/6ad18ce66bd7d205ec7eaa73.png)
まじめな自己紹介14年9月17日水曜日7

![image](https://scrapbox.io/files/6ad18ce76bd7d205ec7eaa95.png)
まじめな自己紹介•サイボウズ・ラボ14年9月17日水曜日7

![image](https://scrapbox.io/files/6ad18ce76bd7d205ec7eaaba.png)
まじめな自己紹介•サイボウズ・ラボ•次世代のグループウェアの基盤となる技術を中長期視点で研究開発14年9月17日水曜日7

![image](https://scrapbox.io/files/6ad18ce86bd7d205ec7eaadf.png)
まじめな自己紹介•サイボウズ・ラボ•次世代のグループウェアの基盤となる技術を中長期視点で研究開発•ワンライナーは書いていません14年9月17日水曜日7

![image](https://scrapbox.io/files/6ad18ce96bd7d205ec7eaaff.png)
サイボウズにおけるPython利用シーン•自動化•インフラ•解析14年9月17日水曜日8

![image](https://scrapbox.io/files/6ad18cea6bd7d205ec7eab20.png)
自動化•VM・ストレージ・各種設定の管理•テスト:記述するのもモックを作るのも楽•Jenkinsのスクリプトとして→RequestsでkintoneのAPIを叩いたり14年9月17日水曜日9

![image](https://scrapbox.io/files/6ad18cea6bd7d205ec7eab4e.png)
インフラ14年9月17日水曜日10

![image](https://scrapbox.io/files/6ad18ceb6bd7d205ec7eab7c.png)
Remote Backup 14年9月17日水曜日[https://enterprise.cybozu.com/topics131111/](https://enterprise.cybozu.com/topics131111/) 11

![image](https://scrapbox.io/files/6ad18cec6bd7d205ec7eaba2.png)
P2P automatic failure recovery system 14年9月17日水曜日[http://developer.cybozu.co.jp/tech/?p=5799](http://developer.cybozu.co.jp/tech/?p=5799) 12

![image](https://scrapbox.io/files/6ad18ced6bd7d205ec7eabbc.png)
P2P automatic failure recovery system 14年9月17日水曜日[http://developer.cybozu.co.jp/tech/?p=5799](http://developer.cybozu.co.jp/tech/?p=5799) 13

![image](https://scrapbox.io/files/6ad18ced6bd7d205ec7eabd3.png)
インフラ•性能が要求される部分はC++やJava •Pythonでそれらのコンポーネントをつなぎ合わせる14年9月17日水曜日14

![image](https://scrapbox.io/files/6ad18cee6bd7d205ec7eabf0.png)
解析14年9月17日水曜日15

![image](https://scrapbox.io/files/6ad18cef6bd7d205ec7eac08.png)
解析•データの収集14年9月17日水曜日15

![image](https://scrapbox.io/files/6ad18cf06bd7d205ec7eac30.png)
解析•データの収集•クレンジング・フィルタリング14年9月17日水曜日15

![image](https://scrapbox.io/files/6ad18cf06bd7d205ec7eac54.png)
解析•データの収集•クレンジング・フィルタリング•統計処理もNumPy・SciPyでお手軽14年9月17日水曜日15

![image](https://scrapbox.io/files/6ad18cf16bd7d205ec7eac7c.png)
解析•データの収集•クレンジング・フィルタリング•統計処理もNumPy・SciPyでお手軽from scipy.stats import chi2_contingency chi2_contingency(data) 14年9月17日水曜日15

![image](https://scrapbox.io/files/6ad18cf26bd7d205ec7eaca3.png)
サイボウズにおけるPython利用シーン•自動化•インフラ•解析→具体例を話します14年9月17日水曜日16

![image](https://scrapbox.io/files/6ad18cf36bd7d205ec7eacc7.png)
14年9月17日水曜日17

![image](https://scrapbox.io/files/6ad18cf46bd7d205ec7eace8.png)
おすすめグラフChart recommendation •データからグラフを作る•どんなグラフを作るか選択肢が色々•コンピュータが支援14年9月17日水曜日[http://developer.cybozu.co.jp/tech/?p=3874](http://developer.cybozu.co.jp/tech/?p=3874) 18

![image](https://scrapbox.io/files/6ad18cf56bd7d205ec7ead15.png)
Recommend charts using statistics of data distribution 14年9月17日水曜日19

![image](https://scrapbox.io/files/6ad18cf66bd7d205ec7ead3f.png)
おすすめグラフChart recommendation •プロトタイプにFlask、NumPy •標準ライブラリのcollectionsも便利•製品版はJavaScriptで実装されてます14年9月17日水曜日[http://developer.cybozu.co.jp/tech/?p=3874](http://developer.cybozu.co.jp/tech/?p=3874) 20

![image](https://scrapbox.io/files/6ad18cf76bd7d205ec7ead6e.png)
What is groupware? 14年9月17日水曜日21

![image](https://scrapbox.io/files/6ad18cf86bd7d205ec7ead95.png)
What is groupware? Group + Software 14年9月17日水曜日21

![image](https://scrapbox.io/files/6ad18cf96bd7d205ec7eadba.png)
Augmenting Human Intellectソフトウェアによって人間の能力を増強するエンゲルバート"Augmenting Human Intellect: A Conceptual Framework" (1962) 14年9月17日水曜日22

![image](https://scrapbox.io/files/6ad18cfa6bd7d205ec7eade5.png)
Augmenting Group Intellectソフトウェアによって集団の能力を増強する=グループウェア14年9月17日水曜日23

![image](https://scrapbox.io/files/6ad18cfb6bd7d205ec7eae14.png)
word2vec文章を与えるとコンピュータが単語の意味を理解する14年9月17日水曜日24

![image](https://scrapbox.io/files/6ad18cfb6bd7d205ec7eae3f.png)
人間コンピュータ14年9月17日水曜日25

![image](https://scrapbox.io/files/6ad18cfc6bd7d205ec7eae69.png)
人間+コンピュータ=増強された人間人間14年9月17日水曜日26

![image](https://scrapbox.io/files/6ad18cfd6bd7d205ec7eae8d.png)
14年9月17日水曜日27

![image](https://scrapbox.io/files/6ad18cfe6bd7d205ec7eaeb4.png)
14年9月17日水曜日28

![image](https://scrapbox.io/files/6ad18cff6bd7d205ec7eaeda.png)
14年9月17日水曜日“やる気の出るアドバイス"で検索29

![image](https://scrapbox.io/files/6ad18d006bd7d205ec7eaf11.png)
14 channels brain wave sensor 14年9月17日水曜日30

![image](https://scrapbox.io/files/6ad18d016bd7d205ec7eaf29.png)
Human→Machine keyboard switch mouse camera touch panel (multi-touch) scanner Machine→Human paper CRT liquid crystal e-ink 3D TV HMD 14年9月17日水曜日31

![image](https://scrapbox.io/files/6ad18d016bd7d205ec7eaf4c.png)
Machine→Human paper CRT liquid crystal e-ink 3D TV HMD book e-book 14年9月17日水曜日32

![image](https://scrapbox.io/files/6ad18d026bd7d205ec7eaf7c.png)
人間増強の四要素•1:人工物(Artifacts):コンピュータ、ソフトウェア、etc. •2:言語(Language):概念を表す専門用語、デザパタ、etc. •3:方法論(Methodology):問題解決のための手順、戦略、etc. •4:教育(Training): 13を使うスキルを身につける14年9月17日水曜日エンゲルバート"Augmenting Human Intellect: A Conceptual Framework" (1962) 33

![image](https://scrapbox.io/files/6ad18d036bd7d205ec7eafa0.png)
人間増強の四要素•1:人工物(Artifacts):コンピュータ、ソフトウェア、etc. •2:言語(Language):概念を表す専門用語、デザパタ、etc. •3:方法論(Methodology):問題解決のための手順、戦略、etc. •4:教育(Training): 13を使うスキルを身につける14年9月17日水曜日エンゲルバート"Augmenting Human Intellect: A Conceptual Framework" (1962) 34

![image](https://scrapbox.io/files/6ad18d046bd7d205ec7eafbc.png)
theme of this conference: Rediscover with Python 14年9月17日水曜日35

![image](https://scrapbox.io/files/6ad18d056bd7d205ec7eafde.png)
How to discover? →Methodology to ﬁnd unknown 14年9月17日水曜日36

![image](https://scrapbox.io/files/6ad18d066bd7d205ec7eb007.png)
14年9月17日水曜日37

![image](https://scrapbox.io/files/6ad18d076bd7d205ec7eb02a.png)
14年9月17日水曜日38

![image](https://scrapbox.io/files/6ad18d086bd7d205ec7eb059.png)
14年9月17日水曜日39

![image](https://scrapbox.io/files/6ad18d096bd7d205ec7eb084.png)
How to discover? →Change Perspective 14年9月17日水曜日40

![image](https://scrapbox.io/files/6ad18d0a6bd7d205ec7eb0b1.png)
Change Perspective •どんな視点で物事を見ても、かならず見えていない部分がある•見えてない部分を見るために視点を変える14年9月17日水曜日41

![image](https://scrapbox.io/files/6ad18d0b6bd7d205ec7eb0e4.png)
known (cid:15511) unknown 14年9月17日水曜日42

![image](https://scrapbox.io/files/6ad18d0d6bd7d205ec7eb117.png)
明らかに知らない43明らかに知っている14年9月17日水曜日

![image](https://scrapbox.io/files/6ad18d0e6bd7d205ec7eb14a.png)
明らかに知らない不明明らかに知っている14年9月17日水曜日44

![image](https://scrapbox.io/files/6ad18d0f6bd7d205ec7eb17f.png)
盲点(blind spot) •「明らかに知ってる」領域と「明らかに知らない」領域の間に「知らないことを知らない」領域がある。•見えていないのに、見えてないことに気づいていない。それが盲点。14年9月17日水曜日45

![image](https://scrapbox.io/files/6ad18d106bd7d205ec7eb1a5.png)
明らかに知らない明らかに知っている14年9月17日水曜日「どこまで知っているのか」を明らかにする46

![image](https://scrapbox.io/files/6ad18d116bd7d205ec7eb1c4.png)
明らかに知らない明らかに知っている14年9月17日水曜日←盲点blindspot 47

![image](https://scrapbox.io/files/6ad18d126bd7d205ec7eb1e2.png)
明らかに知らない明らかに知っている14年9月17日水曜日←盲点blindspot 48

![image](https://scrapbox.io/files/6ad18d136bd7d205ec7eb209.png)
How to ﬁnd blind spot? 14年9月17日水曜日49

![image](https://scrapbox.io/files/6ad18d146bd7d205ec7eb233.png)
Comparison History Experience 14年9月17日水曜日50

![image](https://scrapbox.io/files/6ad18d156bd7d205ec7eb260.png)
Comparison History Experience + Abstraction Communication 14年9月17日水曜日51

![image](https://scrapbox.io/files/6ad18d166bd7d205ec7eb28d.png)
How to ﬁnd blind spot? Comparison History Experience Abstraction Communication 14年9月17日水曜日52

![image](https://scrapbox.io/files/6ad18d176bd7d205ec7eb2b2.png)
Comparison •例:複数言語を比較することで気づく「あれ?Rubyでは0は真なのか?! Pythonでは偽だよな?!」「言語によって何が真か異なるのか?」「他の言語ではどうなってるんだろう?」「Pythonではどう定義されている?」14年9月17日水曜日object.__nonzero__(self) Called to implement truth value testing and the built-in operation bool(); 53

![image](https://scrapbox.io/files/6ad18d196bd7d205ec7eb2d3.png)
History •例:歴史を追うことで盲点に気づく「PythonってなんでNew-styleクラスとそうでないのの2つあるの? →歴史を知る→型とクラスを融合する目的のためにメソッドの名前解決の順序の決め方を変える必要があったことに気づく14年9月17日水曜日Unifying types and classes in Python 2.2 | Python.org [https://www.python.org/download/releases/2.2.3/descrintro](https://www.python.org/download/releases/2.2.3/descrintro) 54

![image](https://scrapbox.io/files/6ad18d196bd7d205ec7eb2fe.png)
Experience •実際に使うことで盲点に気づく「あれ?1/2は0.5になると思ったが0になったぞ?」14年9月17日水曜日PEP 238 -- Changing the Division Operator [http://legacy.python.org/dev/peps/pep-0238/](http://legacy.python.org/dev/peps/pep-0238/) 55

![image](https://scrapbox.io/files/6ad18d1a6bd7d205ec7eb336.png)
Abstraction •具体例を抽象化したものに触れることで自分の経験を言語化する「ああ、なんとなく使っていたこの書き方って、Mediatorパターンって名前がついていたのか!」14年9月17日水曜日56

![image](https://scrapbox.io/files/6ad18d1b6bd7d205ec7eb35f.png)
Communication •経験の異なる他人と会話することで盲点に気づく「こういう問題に困ってんだよね」「それこうしたらいいんじゃない?」「なるほど、その発想はなかった!」「いや、GUIでは普通の発想だよ」「俺サーバ周りが専門だからなぁ」14年9月17日水曜日57

![image](https://scrapbox.io/files/6ad18d1c6bd7d205ec7eb37f.png)
How to ﬁnd blind spot? Comparison History Experience Abstraction Communication 14年9月17日水曜日58

![image](https://scrapbox.io/files/6ad18d1c6bd7d205ec7eb3a7.png)
Communication 14年9月17日水曜日59

![image](https://scrapbox.io/files/6ad18d1d6bd7d205ec7eb3ca.png)
Ofﬁce Hour 13:00-13:30 Blog, Mail see [http://nhiro.org/](http://nhiro.org/) 14年9月17日水曜日60

![image](https://scrapbox.io/files/6ad18d1e6bd7d205ec7eb408.png)
Q&A ↓質問を思い出すのにとても役に立ちました!ありがとう! PyCon JP 2014 Day 3感想とノート#pyconjp |こえむの編集後記[http://www.koemu.com/blog/2014/09/15/pycon-jp-2014-day3/](http://www.koemu.com/blog/2014/09/15/pycon-jp-2014-day3/) 14年9月17日水曜日61

![image](https://scrapbox.io/files/6ad18d1f6bd7d205ec7eb43a.png)
Q:「盲点に気づくチャンス」となる情報を見ても認知的不協和を起こして「そんなはずはない」と思ってしまう人がいるのでは。組織のaugmentを考える上ではそういう人をどうすればよいだろうか?どう啓蒙する? 14年9月17日水曜日62

![image](https://scrapbox.io/files/6ad18d206bd7d205ec7eb470.png)
A:まさにその点に対して答えようとしている「U理論」について9/24から京都大学サマーデザインスクールで解説する予定なのでその資料を…[http://www.design.kyoto-u.ac.jp/sds2014/ja/theme01.html](http://www.design.kyoto-u.ac.jp/sds2014/ja/theme01.html) 63 14年9月17日水曜日

![image](https://scrapbox.io/files/6ad18d216bd7d205ec7eb4a4.png)
A:言いたいことは2点ある。まず「他人をどう変えるか」というスタンスではうまくいかない。自分が変わる必要がある。14年9月17日水曜日64

![image](https://scrapbox.io/files/6ad18d226bd7d205ec7eb4dc.png)
A:次に「見えているのに見ていない」状態にハマることは自分も含めてよくあること、と気づくこと。14年9月17日水曜日65

![image](https://scrapbox.io/files/6ad18d246bd7d205ec7eb512.png)
A:最初は小さなものでよいので、その気付きから有益な結果が得られる「成功体験」を積むこと。これが自信につながる。14年9月17日水曜日66

![image](https://scrapbox.io/files/6ad18d256bd7d205ec7eb53d.png)
PDCAサイクルとU曲線の関係U曲線補足スライドU曲線状態行動14年9月17日水曜日67 C・オットー・シャーマー「U理論」

![image](https://scrapbox.io/files/6ad18d266bd7d205ec7eb55f.png)
PDCAサイクルとU曲線の関係U曲線補足スライドU曲線←見えているのに思い込みにとらわれてきちんと見てない状態状態行動14年9月17日水曜日68 C・オットー・シャーマー「U理論」

![image](https://scrapbox.io/files/6ad18d286bd7d205ec7eb587.png)
PDCAサイクルとU曲線の関係U曲線補足スライドU曲線←見てはいるが、自分の視点からだけ。状態行動「奴らはしないから」と考えたりする。自己と他者の間に境界線を引いて14年9月17日水曜日69 C・オットー・シャーマー「U理論」

![image](https://scrapbox.io/files/6ad18d296bd7d205ec7eb5a7.png)
Q:モデリングをどうやってやるかも大事なのではないか? 14年9月17日水曜日70

![image](https://scrapbox.io/files/6ad18d2a6bd7d205ec7eb5c0.png)
A:はい、大事です。14年9月17日水曜日71

![image](https://scrapbox.io/files/6ad18d2b6bd7d205ec7eb5d5.png)
この特集の3章がまるまるその内容ですWEB上で読めます14年9月17日水曜日[http://gihyo.jp/lifestyle/feature/01/engineer-studying](http://gihyo.jp/lifestyle/feature/01/engineer-studying) 72

![image](https://scrapbox.io/files/6ad18d2c6bd7d205ec7eb5e5.png)
A:経験から仮説が作られる。「理解した」という気持ちも仮説。仮説は実験によって検証する必要がある。理解に基づいて行動し結果を確認する14年9月17日水曜日73

![image](https://scrapbox.io/files/6ad18d2e6bd7d205ec7eb608.png)
A:行動した結果が予想と異なった場合はモデルを修正する必要がある。これを繰り返していくことで「正しい可能性の高い」モデルを作り、それを組み合わせることでより大きなモデルを作る。これが一つの方法論14年9月17日水曜日74

![image](https://scrapbox.io/files/6ad18d2e6bd7d205ec7eb625.png)
A:もう一つの方法論として実験が容易でない人文科学では、KJ法やグラウンデッド・セオリーが使われる。14年9月17日水曜日75

![image](https://scrapbox.io/files/6ad18d2f6bd7d205ec7eb63c.png)
A:まずインタビューなどで大量にデータを集め、それを自分の偏見で「これはノイズだ」とフィルタリングすることなく一覧できるようにする14年9月17日水曜日76

![image](https://scrapbox.io/files/6ad18d306bd7d205ec7eb654.png)
A:人間の作業記憶は7つくらいしかないが、データを紙に書いて机の上に広げれば100とか200とかを見ることができる14年9月17日水曜日77

![image](https://scrapbox.io/files/6ad18d316bd7d205ec7eb66b.png)
A: 100のデータを一覧できる状態を作った上で、机の上で動かすことでモデルを組み立てていく、これがKJ法(会場では言いそこねたが、[[既存の構造]]をトップダウンに当てはめるのではなく、データからボトムアップで構造を組み立てていくのも重要なポイント) (ちなみに上記で紹介した拙著書籍・特集記事は14年9月17日水曜日78 KJ法でモデル化されている)

![image](https://scrapbox.io/files/6ad18d316bd7d205ec7eb685.png)
Oﬃce Hourでの質問Q:盲点に気づく5つの方法は並列ではなく、時間軸で前後関係があるのではないか? 14年9月17日水曜日79

![image](https://scrapbox.io/files/6ad18d326bd7d205ec7eb696.png)
A:それは盲点だった!確かに抽象はいきなり最初から使うことはできない。プログラミングの経験がない人がデザインパターンの本を読んでも自分の経験と結びつかない。14年9月17日水曜日80

![image](https://scrapbox.io/files/6ad18d336bd7d205ec7eb698.png)
Q:テスタの間でテストのノウハウを共有したいがどうしたらいいか(詳細な状況説明は省略) 14年9月17日水曜日81

![image](https://scrapbox.io/files/6ad18d346bd7d205ec7eb6a8.png)
A:言語化されていない知識をどうやって共有するかという問題だと思える。一つの方法論は「一緒に作業」だ。14年9月17日水曜日82

![image](https://scrapbox.io/files/6ad18d346bd7d205ec7eb6bc.png)
A:一緒に作業することでノウハウを言語化しないまま共有することができる。更に「操作せずに指示する人と操作する人」を分ければ指示するために知識の言語化が促される14年9月17日水曜日参考文献“凡才の集団は孤高の天才に勝る" 83

![image](https://scrapbox.io/files/6ad18d356bd7d205ec7eb6ce.png)
A:言語化が行われて初めて、マニュアル化などができるようになる。言語化は結構難しいタスクなので、そのスキルを鍛えずにいきなり個々人に任せるとうまくいかない。14年9月17日水曜日84

![image](https://scrapbox.io/files/6ad18d366bd7d205ec7eb6e4.png)
言語化されていない知識補足スライドこのスパイラルを回すことで知識が創造される『知識創造企業』p93 85 14年9月17日水曜日

![image](https://scrapbox.io/files/6ad18d366bd7d205ec7eb6fa.png)
言語化されていない知識補足スライド↑ペアプロ・共同作業はここに相当するこのスパイラルを回すことで知識が創造される『知識創造企業』p93 86 14年9月17日水曜日

![image](https://scrapbox.io/files/6ad18d376bd7d205ec7eb706.png)
Q:私は情報の言語化のためのテンプレートを作っている。質問に答えていくと必要な情報が揃う。14年9月17日水曜日87

![image](https://scrapbox.io/files/6ad18d386bd7d205ec7eb71f.png)
A:それは良いアプローチ。「言語化しろ」と言われてできない人でも、具体的に質問をされると答えられることがよくある。適切な質問を投げかけることは重要。14年9月17日水曜日88

![image](https://scrapbox.io/files/6ad18d396bd7d205ec7eb73d.png)
A:そういう意味でテンプレート化にはメリットがある。しかし、テンプレートで表現できない情報が捨てられてしまうデメリットに気をつける必要がある。新しい重要な情報は定型化されていない。14年9月17日水曜日89

