---
title: "東工大ホームカミングデー「AIとMOT」"
---

このページ、iPhoneのSalariではスライド画像が表示されるが、PCのChromeからは表示されない。[[最新のChromeはHTTPSのページでHTTPの画像表示を許さない]]のせい、画像の置き場所を変えねば。

スライド
![image](http://nhiro.org/titech_hcd/page-01.png)
東工大MOTホームカミングデー「AIとMOT」2018-05-26サイボウズラボ主幹研究員一般社団法人未踏理事東工大MOT 2011入学-2014修了2018から特定准教授西尾泰和

![image](http://nhiro.org/titech_hcd/page-02.png)
Facebookグループ2講演資料の共有質疑・コメントその他なんでも

![image](http://nhiro.org/titech_hcd/page-03.png)
今回の目的3この講演を聞いた人が経済的価値を生み出す確率を上昇させる

![image](http://nhiro.org/titech_hcd/page-04.png)
AlphaGo 4初めてプロを破った囲碁プログラム

![image](http://nhiro.org/titech_hcd/page-05.png)
コンピュータが人間を超える?! 5人間コンピュータ

![image](http://nhiro.org/titech_hcd/page-06.png)
Deep Learningが期待を集めた6縦軸:期待

![image](http://nhiro.org/titech_hcd/page-07.png)
出典表示7 [https://www.gartner.com/smarterwithgartner/top-trends-in-the-gartner-hype-cycle-for-](https://www.gartner.com/smarterwithgartner/top-trends-in-the-gartner-hype-cycle-for-) emerging-technologies-2017/

![image](http://nhiro.org/titech_hcd/page-08.png)
8 Deep Learningという魔法の杖のような技術で色々な問題が解決するっぽい!

![image](http://nhiro.org/titech_hcd/page-09.png)
事例紹介:駐車難易度予測9 [https://ai.googleblog.com/2017/02/using-machine-learning-to-predict.html](https://ai.googleblog.com/2017/02/using-machine-learning-to-predict.html)

![image](http://nhiro.org/titech_hcd/page-10.png)
駐車難易度予測10 •Google Mapの機能•「この時間にこのエリアで駐車するのは難しい?簡単?」に答える•Deep Learningすごい!

![image](http://nhiro.org/titech_hcd/page-11.png)
Deep Learningは使いません11「ロジスティック回帰で実現しました」その理由(抜粋) •振る舞いが理解しやすい•ノイズに対して耐性が高い•モデルが適切に動いているか検証しやすい

![image](http://nhiro.org/titech_hcd/page-12.png)
ロジスティック回帰12 •1958年に作られた手法•数学的にはDeep Learningではなく薄いニューラルネットに相当する•枯れた手法なので学習の高速化が進んでいる

![image](http://nhiro.org/titech_hcd/page-13.png)
Kaggleによる調査13機械学習コンペティション最大手のKaggleによって大規模な調査が行われた7301人のデータサイエンティストに仕事で使っている機械学習手法を聞いたら…The State of ML and Data Science 2017 | Kaggle [https://www.kaggle.com/surveys/2017](https://www.kaggle.com/surveys/2017)

![image](http://nhiro.org/titech_hcd/page-14.png)
ロジスティック回帰63.5% 14

![image](http://nhiro.org/titech_hcd/page-15.png)
手段の目的化15 •Deep Learningはある種のタスクに対して確かに過去の手法より良い精度を出した•しかし万能の道具ではないし魔法の杖でもない•「Deep Learningで経営を改善しよう」は目的を決める前に道具を決めてて、おかしい

![image](http://nhiro.org/titech_hcd/page-16.png)
AlphaGo 16 •ざっくり規模感を掴んでほしい•もう少し詳しく説明します•細かいバージョン間の違いは説明しません

![image](http://nhiro.org/titech_hcd/page-17.png)
データ量17囲碁のオンライン対戦サーバから得られた16万件の対局から2840万件のデータを作成「盤面の状況」と「次の1手」(その状況で人間がどういう意思決定をしたか)のデータを学習する!

![image](http://nhiro.org/titech_hcd/page-18.png)
学習結果18人間の「次の1手」を正解率57.0%で当てることができた

![image](http://nhiro.org/titech_hcd/page-19.png)
自己対戦でデータを生成19人間同士の対戦で作られた16万件の対局データでは足りないので機械同士で対戦して3000万対局(人間や物理世界の介在なしにデータを集められる、という囲碁の特性を利用)

![image](http://nhiro.org/titech_hcd/page-20.png)
3000万対局とは20人間は1局1時間ぐらいなので、3500年分(不眠不休)

![image](http://nhiro.org/titech_hcd/page-21.png)
学習に使った費用21正確な金額はもちろんわからないが公開されている情報からの推定で約30億円だいぶ雑な推定なので「10億100億だ」ぐらいの捉え方が良いと思う[http://www.itmedia.co.jp/news/articles/1603/24/news058.html](http://www.itmedia.co.jp/news/articles/1603/24/news058.html)

![image](http://nhiro.org/titech_hcd/page-22.png)
まとめ22 •まず「人間が行った判断」のデータを3000万件程度集める•シミュレーションで200倍のデータを集める•この過程に30億円を投資する

![image](http://nhiro.org/titech_hcd/page-23.png)
23なぜやったのか? (経営者目線で考えてみよう)

![image](http://nhiro.org/titech_hcd/page-24.png)
AlphaGoをやる理由は? 24 •ブランディング? •新入社員の教育を兼ねてる? •世界初のことをやると社員のテンションが上がるから? •夢を見せることによって投資を引き出す?

![image](http://nhiro.org/titech_hcd/page-25.png)
期待が高まると投資が増える25縦軸:期待

![image](http://nhiro.org/titech_hcd/page-26.png)
技術のS字発展26ベルカーブS字カーブ積分ハイプカーブS字発展+持続的成長積分

![image](http://nhiro.org/titech_hcd/page-27.png)
予言の自己成就27 •技術のすごさをアピール•未来への期待が高まる•投資が引き出される•それが技術の進歩速度を高める

![image](http://nhiro.org/titech_hcd/page-28.png)
28しかし逆効果も…

![image](http://nhiro.org/titech_hcd/page-29.png)
29 AIに仕事を奪われる恐怖

![image](http://nhiro.org/titech_hcd/page-30.png)
30知識は恐怖の解毒剤Ralph Waldo Emerson “Society and Solitude"

![image](http://nhiro.org/titech_hcd/page-31.png)
31漠然とした概念ではなく具体的な事例に基づいて考えよう

![image](http://nhiro.org/titech_hcd/page-32.png)
事例紹介:三浦市農協の配車予定作成システム32 ref: ICTで社会が変わる事例紹介

![image](http://nhiro.org/titech_hcd/page-33.png)
33「出荷作業8時間を1秒に」三浦市農協で起きた驚異の進化[http://wedge.ismedia.jp/articles/-/12062](http://wedge.ismedia.jp/articles/-/12062)

![image](http://nhiro.org/titech_hcd/page-34.png)
アルゴリズムで8Hの仕事を消す34 •••“農協の業務の中でもやっかいな出荷物の配送予定の作成" “1日8時間かかっていた作業がわずか1秒で済む" “独自のアルゴリズム"このアルゴリズムを作ったのが僕。「出荷作業8時間を1秒に」三浦市農協で起きた驚異の進化[http://wedge.ismedia.jp/articles/-/12062](http://wedge.ismedia.jp/articles/-/12062)

![image](http://nhiro.org/titech_hcd/page-35.png)
“配送予定の作成"とは35 •“翌日に農家から出荷される出荷物の量を把握し、市場などの配送先ごとの出荷数量と、荷物をどの運送会社のトラックにどう積み分けるかを決める。" •配車予定の作成には、中堅職員で8時間、ベテランでも56時間掛かっている。•若い職員「こんなのはさすがにやれない」「出荷作業8時間を1秒に」三浦市農協で起きた驚異の進化[http://wedge.ismedia.jp/articles/-/12062](http://wedge.ismedia.jp/articles/-/12062)

![image](http://nhiro.org/titech_hcd/page-36.png)
“AIが仕事を奪う"って悪いの? 36 •今回は、1日あたり8時間、人間およそ1人分の仕事を奪ったが…•“同農協共販部長補佐の飯島昌祥さんは「労働時間の短縮が一番大きい。職員の負担が減るし、空いた時間を営業などに効率的に使えるので期待している」"とポジティブな意見

![image](http://nhiro.org/titech_hcd/page-37.png)
人口ピラミッド37出典:国立社会保障・人口問題研究所[http://www.ipss.go.jp/site-ad/TopPageData/pyra.html](http://www.ipss.go.jp/site-ad/TopPageData/pyra.html)

![image](http://nhiro.org/titech_hcd/page-38.png)
人口の変化38 1973生西尾('81生)僕や僕より若い世代は毎年人数が減る環境で育ってきた

![image](http://nhiro.org/titech_hcd/page-39.png)
7人に1人いなくなる39今後15年で、20代人口は、67人に1人の割合で減る。

![image](http://nhiro.org/titech_hcd/page-40.png)
7人に1人いなくなると…40今7人チームでやっている仕事は、チームの年齢構成が変わらないなら15年後には6人でやらなければならない仕事量が変わらなければ1人当たりの仕事量は17%アップ月20日×8時間働いている仕事は仕事が17%アップで月に+27時間。毎日残業+1時間か、毎月休日-3日

![image](http://nhiro.org/titech_hcd/page-41.png)
現状維持とは41「今までと同じ仕事の仕方をする」は現状維持ではない。人間の負担が増えて仕事が回らなくなる。現状を維持するには1/7の仕事を"AIに奪われる"か人間の能力を7/6倍にする必要がある。

![image](http://nhiro.org/titech_hcd/page-42.png)
42 ×AIに1/7の仕事が奪われる○AIに1/7肩代わりして頂く○AIを使って人間を16%増強

![image](http://nhiro.org/titech_hcd/page-43.png)
余剰時間の再投資43 •若い人が減っていくトレンド•新しい人の採用がじわじわと難しくなる•「AIで仕事を減らして余剰人員を解雇」という発想は筋悪•AIで仕事を減らして、できた空き時間をより生産的な仕事に再投資•拡大再生産

![image](http://nhiro.org/titech_hcd/page-44.png)
人間コンピュータ

![image](http://nhiro.org/titech_hcd/page-45.png)
[[人間+コンピュータ=増強された人間]]
人間

![image](http://nhiro.org/titech_hcd/page-46.png)
人間+コンピュータ=増強された人間人間

![image](http://nhiro.org/titech_hcd/page-47.png)
増強の具体例47 •コンピュータによる計算能力の強化•インターネットによる伝達能力の強化•検索エンジンによる情報発見能力の強化もっと具体例が知りたいというリクエストがあったのでさらにいくつか紹介しよう

![image](http://nhiro.org/titech_hcd/page-48.png)
自動プログラミング48プログラミングが大変なので自動化しようという発想

![image](http://nhiro.org/titech_hcd/page-49.png)
自動プログラミング以前49「AとBを足したものをCに入れる」をやりたいLOAD 1 ADD 2 STORE 3メモリの1番地にある値を計算用の一時領域にロードメモリの2番地にある値をそれに加算一時領域にある値をメモリの3番地に保存これは話を簡単にするための疑似コードで、実際はもっと複雑です

![image](http://nhiro.org/titech_hcd/page-50.png)
自動プログラミング50「AとBを足したものをCに入れる」をC = A + B;という記法で書くことにする。コンピュータがこの記法を読み取ってLOAD 1; ADD 2; STORE 3;を自動生成する「数式変換システム」

![image](http://nhiro.org/titech_hcd/page-51.png)
19541957年FORTRAN 51 •FORmula TRANslation system •現代のほぼすべてのプログラマが使う「プログラミング言語」のはしり•抽象レベルの高い数式で書いた指示を抽象レベルの低い機械語で書いた指示に変換するシステム(自動プログラミング*) *“The Fortran Automatic Coding System for the IBM 704" (1956)システムができたのが54年、このマニュアルができたのが56年、一般に入手可能になったのが57年。

![image](http://nhiro.org/titech_hcd/page-52.png)
スクリプト言語の誕生52 30年ほど前にメジャーなC言語などより低速なPerl, Python, PHP, Rubyなどの言語が誕生実行速度C言語Python時間

![image](http://nhiro.org/titech_hcd/page-53.png)
破壊的イノベーション53「イノベーションのジレンマ」p.10

![image](http://nhiro.org/titech_hcd/page-54.png)
スクリプト言語54 •コンピュータが高速化した•遅いプログラミング言語でも顧客の需要を満たしうるようになった•「実行速度は遅いが、実装に掛かる時間が少ない」筆記体(script)の走り書きのような言語

![image](http://nhiro.org/titech_hcd/page-55.png)
機械学習が与える影響55 •プログラムの大部分は条件判断•人間が「どういう条件か」を明確にしそれをコンピュータに伝える•しかし課題によっては「条件を明確化すること」が難しい(囲碁、画像認識、…) •機械学習は…

![image](http://nhiro.org/titech_hcd/page-56.png)
機械学習が与える影響56機械学習は、状況を表すデータと「その状況の時に人間はどう判断するのか」のデータを与えて学習させることで、コンピュータが条件判断できるようになる手法人間は条件を明確化しないでよい。注:教師あり学習に限定して説明しています。

![image](http://nhiro.org/titech_hcd/page-57.png)
確実性を犠牲にコストを削減57 •人間が条件を明確化しないので「条件通りに動いているか?」という問いが無意味•「検証データの9割は正しく判断できますね」みたいなことしか言えない•確実性を犠牲にして仕様記述コストを下げる

![image](http://nhiro.org/titech_hcd/page-58.png)
まとめ58 •自動プログラミング•スクリプト言語•機械学習共通しているのは人のコストの削減

![image](http://nhiro.org/titech_hcd/page-59.png)
アカデミア視点とビジネス視点59ビジネス視点から言えば•コストの減少によって•新たな財貨やその生産方法が•「商業的に実現可能な範囲」に入る現象アカデミアの評価軸とビジネスの評価軸は違う

![image](http://nhiro.org/titech_hcd/page-60.png)
アカデミアとビジネスの違い60アカデミア•データが公開されている•枯れた技術はとっくの昔に調査済み•新しい手法を考案して精度を競い合うビジネス•データが公開されてない枯れた技術を使う

![image](http://nhiro.org/titech_hcd/page-61.png)
ビジネスの評価軸61顧客価値新規性ではない

![image](http://nhiro.org/titech_hcd/page-62.png)
顧客価値を体感するための小問62ある宝石の原石は、割ると1/2の確率で宝石が入っていて2万円で売れる。原石は1つ9500円で買える。原石は硬いので1日に20個しか割れないQ1: 1日に稼げる収益の期待値はいくらか仕入れ原価原石1/2宝石9500円×1/2売上2万円0円

![image](http://nhiro.org/titech_hcd/page-63.png)
A1収益の期待値63 A1: 1/2の確率で20000円手に入るので、1個あたりの収入の期待値は10000円。1個あたりの仕入れ価格は9500なので、1個あたりの収益は500円。1日に20個処理できるので、1日あたりの収益は10000円。原価9500円売上1万円1つあたり500円の利益

![image](http://nhiro.org/titech_hcd/page-64.png)
Q2加工速度二倍の装置64 Q2:原石を人間の2倍の速度で割る機械を手に入れたとする。つまり、1日に割ることができる原石の数が20個から40個に増えたとする。収益の期待値はいくら増えるか?

![image](http://nhiro.org/titech_hcd/page-65.png)
A2加工速度二倍の装置65 A2:原石1個あたり500円の利益なのは変わらない。1日に処理できる量が20個から40個に増える。20個増えるので、利益は1万円増える。原価9500円売上1万円1つあたり500円の利益

![image](http://nhiro.org/titech_hcd/page-66.png)
Q3 60%の識別器66 Q3: 60%の確率で宝石の入った原石を当てる識別器*が買えるとする。収益の期待値はいくら増えるか?仕入れ原価原石60%宝石9500円×40%売上2万円0円*原石を買う前に使うことで「60%の確率で宝石が入っている原石」を9500円で手に入れられるようになるとします。お店の人が嫌がりそう、という点は今回は気にません。またQ2の機械は手に入っておらず、1日に割れる数は20個のままとします。

![image](http://nhiro.org/titech_hcd/page-67.png)
A3: 60%の識別器67 60%の確率で20000円手に入るので、1個あたりの収入の期待値は12000円。1個あたりの仕入れ価格は9500円なので、1個あたりの収益は2500円。1日に20個処理できるので1日あたりの収益は5万円。4万円増える。原価9500円売上12000円1つあたり2500円の利益

![image](http://nhiro.org/titech_hcd/page-68.png)
つまり68この問題設定では、「加工速度を2倍にする装置」は顧客の利益を1万円増やし、「精度60%の識別器」は顧客の利益を4万円増やす。「精度60%の識別器」が「加工速度を2倍にする装置」の4倍の顧客価値を持っている。

![image](http://nhiro.org/titech_hcd/page-69.png)
まとめ69 •ビジネス視点では顧客価値が大事•顧客価値は「手法の新規性」ではない•顧客価値と精度はイコールではない

![image](http://nhiro.org/titech_hcd/page-70.png)
強制オープンイノベーション70 •2017年、Appleが初の機械学習論文を発表•Appleですら社員の「発表したい」という要望にNOと言えなくなった•機械学習技術をクローズドに独占できない•「オープンイノベーションは、選択肢ではない。事実だ」**元ネタは2009年ライス国務長官の"Globalization is not a choice but a fact"

![image](http://nhiro.org/titech_hcd/page-71.png)
専門技術の市場調達71専門技術を市場調達しようと考える企業も多いしかし専門家の能力は観測が困難評価能力がないと…(ここでオフレコの酷い話をする)

![image](http://nhiro.org/titech_hcd/page-72.png)
契約理論72契約当事者間で情報の非対称性がある場合にどういう解決策があるか•シグナリング•スクリーニング

![image](http://nhiro.org/titech_hcd/page-73.png)
シグナリング73情報を持っている側がやる行為。たとえば「能力」は観測が困難そこで「能力」を示すことができるような「シグナル」を獲得しようとする

![image](http://nhiro.org/titech_hcd/page-74.png)
シグナリング74なぜAppleの社員は論文発表をしたいのか?それは論文発表実績が「シグナル」となり、Apple以外に転職する場合に有利だから。専門家を市場調達する場合、その専門家はシグナルを出せることを要求してくる可能性が高い。

![image](http://nhiro.org/titech_hcd/page-75.png)
スクリーニング75情報を持っていない側がやる行為。たとえば営業マンに対して「低い固定給+歩合報酬」を提示する。能力の低い営業マンは勝手に避けてくれる。しかし…

![image](http://nhiro.org/titech_hcd/page-76.png)
機械学習と成果報酬76機械学習は「実際のデータで試してみないと成果が出るかどうかわからない」という成果報酬と相性の悪い特徴がある。機械学習の専門家側としては成果報酬のプロジェクトは引き受けたくない。(ビジネス側の出してくるデータが汚いと自分の能力と無関係に成果が出なくなる)成果を確約する請負契約ですら結びたくない。

![image](http://nhiro.org/titech_hcd/page-77.png)
スモールスタート77能力の高い専門家ほど得をするような契約形態を模索しなければならない。まだ完全な解決策は考案できていないが1つの案は最初の一歩の契約を小さくし「うまくいきそうと双方が合意したら延長」とする戦略。専門家の側としては筋悪なプロジェクトに長期間拘束されることもないし、能力が高い方が延長に到る確率が高い。

![image](http://nhiro.org/titech_hcd/page-78.png)
レベニューシェア78もう一つの戦略がレベニューシェア、プロジェクトによって得られる利益を専門家と定率でシェアする方法。利益を出すことに対して両者が協力する。だが、専門家側としては、自分の技能以外に運用側の能力によって成果が変動するのでレベニューシェア単独の契約は引き受けづらいもうひとひねりが必要そう。

![image](http://nhiro.org/titech_hcd/page-79.png)
まとめ79 •強制的にオープンイノベーション•専門技能を市場調達する際には情報の非対称性の問題が発生する•契約理論はより良い契約のために有益な示唆を与えてくれる

![image](http://nhiro.org/titech_hcd/page-80.png)
全体まとめ80 •手段を目的化しない。•AIは仕事を奪うのではなく人間を増強する=人間の支払う時間コストの削減•アカデミアとビジネスの評価軸の違い。顧客価値≠新規性・精度


