---
title: "Majority Judgement勉強会"
---

2021-07-09 [[サイボウズラボ勉強会]]
- 3行にまとめると
    - 多数決という「複数人で意思決定をするためのメカニズム」に深刻な不具合があることは研究者の間では広く知られている
    - 研究者は「[[耐戦略性]]」を良い特徴だと考えている。これは「ウソをついても得しない」というもの。[[アホはいいけど、ウソはだめ]]的な価値観を、意思決定メカニズム自体に持たせようというアプローチ
    - 「みんなで6段階評価して中央値が一番良いものを選ぶ」([[Majority Judgement]])が耐戦略性を持つことが2007年に報告された。今日はそれを紹介する
- 今回ざっくり知るための知識を前に持ってきて、数学的・学術的な話は後にした
- 前回の話: [[メカニズムデザイン勉強会]]

[[票割れ]]の問題
- 「候補から一つ選んで多数決」で「その決定を好まない人が過半数」な決定がされてしまう状況を紹介する
- その状況でMajorty Judgementでは多数派の好む意思決定ができることを示す
- 状況設定
    - ある議題Pについて、選択肢P1がいい人が40%、選択肢P2がいい人が60%いる
    - 一方、Pほど重視されてない議題Qがあって、これは選択肢Q1もQ2も50%ずつ支持されている
    - 候補者が3人いる。A: (P1, Q1), B: (P2, Q1), C: (P2, Q2)
    - ![image](https://gyazo.com/d84911dd7a82029d0a57ea4dcc0fc5e0/thumb/1000)
- 多数決投票を行う
    - 仕組み: 各投票者は自分の意見に最も近い意見の人を一人選んで投票する
    - ![image](https://gyazo.com/2e2915f11f376e2627853128931cf0f5/thumb/1000)
    - 候補者BとCはそれぞれ30%の票を得る
    - 自分の希望と一致する候補者がいなかった投票者(P1Q2)は、意見の近い候補者Aに投票する
    - ![image](https://gyazo.com/3b05c765cabd59547f5b0097ab8715bf/thumb/1000)
    - 結果、Aが40%の票を得て1位になる
        - P2が選ばれて欲しい人が60%だったのにP1が選ばれてしまった
        - 多数決で過半数が不幸になることがある
    - 何がいけないのか
        - Bを選んだ人が「AになるくらいならCのほうがマシ」と思ってたとしても候補者一人を指定する方式では表現する方法がない
        - Bへの投票は「BでないならAでもCでもいい」に相当する
    - 候補者側の歪み
        - 本人が真に良いと思ってる選択肢ではなく、他の候補者が選んでない選択肢をアピールした方が票が集まりやすい
        - 真実と異なる表明をすること(ウソをつくこと)を促すメカニズムになっている
    - 投票者側の歪み
        - B派の人がC派の人に「このままだと票が割れてAが勝ってしまう！CではなくBに投票するんだ！」と勧誘することがある
        - 自分が真に良いと思ってる候補者ではない人に投票する(ウソをつく)ことを促す行動
    - 耐戦略性
        - 多数決は戦略的操作ができる
            - 戦略的操作とは、真実と異なる表明をすることによって帰結を自分にとってより好ましいものにすること
            - ウソをついた方が得だからウソをつく
        - =多数決は耐戦略性がない
        - 耐戦略性のある社会的選択メカニズム(みんなの意見を持ち寄って複数の選択肢から一つ選ぶ仕組み)は可能か？
- Majorty Judgementを行う
    - 仕組み: みんなで6段階評価して中央値が一番良いものを選ぶ
        - 6という数の意味に関しては後述
    - 例えば「6:とてもよい、5:よい、4:どちらかといえばよい、3:どちらかといえば悪い、2:悪い、1:とても悪い」の6段階
    - 投票者がすべての候補者を6段階評価する
        - ![image](https://gyazo.com/c16a8d2a92c8e4cb31b1588a3f1c39fe/thumb/1000)
    - 集計
        - ![image](https://gyazo.com/eaaa33fe506c256e32a2565fba348613/thumb/1000)
        - Aは「6:とてもよい」20%「5:よい」20%「2:悪い」30%なので中央値は「2:悪い」
        - Bは「6:とてもよい」30%「5:よい」30%なので中央値は「5:よい」(Cも全く同じ)
        - よってBとCが同率一位になる
    - Majorty Judgementはウソをついて自分がこのむ方向に社会的評価を動かすことができない(後述)

変える変えない現象
- 関連する話
    - 例えば会社のオフィスの一部を別の目的に使えるように変えようという話が出たとする
    - どう変えるかについて議論をして色々な案が出た
    - それぞれの案が譲らなくて、じゃあ社員投票で決めよう、という話になった
    - その投票項目にうっかり「変えない」を入れてしまった
    - 構図: A:変えない、B:変える、C:変える
    - 変える票がBとCに割れ、投票の結果「変えない」が選ばれてしまった
    - 「あれれ？変えたいという意見が多数派だったはずなのに？？」
- 変える方法は複数あるが、変えない方法は一通りなので、こういう投票をしたら「変えない」が選ばれがち
    - 例えば「変える/変えない」の二択で先に投票してしまうとか、「変えることは良いことだ」的な社風があるとかでないと、変化しない会社になってしまう
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q: 「B案に変えたいが、C案になるくらいら変えない(A案)」という人(と逆にCが良くてBよりはAがいい人)がたくさんいたら「変えない」になりうる？
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>なりうる
    - 例
        - B6 A4 C2 40%
        - C6 A4 B2 40%
        - A6 B2 C2 20%
    - これを集計すると
        - A案 6 20％ 4 80%
        - B案 6 40% 2 60%
    - A が「4: どちらかといえば良い」で選ばれる

実際の応用を考える
- 6段階評価はWebUIでの表現も難しくないし、ユーザの操作も難しくない
- 「一人を選ぶ投票に比べて時間がかかるのでは？」
    - 著者らはフランス大統領選の時に投票所の脇で実際の12人の候補者を対象としてMJの実証実験をした
        - ほとんどの被験者は1分未満で投票した
            - 1候補者あたり5秒未満
            - 各候補の6段階評価なので、各候補者ごとに判断できる。「他の候補者と比べてどちらがマシか」とか考えなくてよい
        - 「この候補者はダメだ」と表明できることで投票者の満足度が高かった
            - 多数決のところで説明したこれと関係する
                - > Bへの投票は「BでないならAでもCでもいい」に相当する
            - 投票者はしばしば「BでもCでもいいけど、Aだけはダメだ」という意見を持つが、「候補から一つ選んで多数決」の仕組みではこれを伝えられない
- 「6段階」の6の意味
    - 数学的なモデルとしてはいくつでもいい
    - 「0から100で点数をつけて」でもよい
    - フランス大統領選の実験で、12候補者を6段階で評価したが、86%の人が5種類しか使わなかった
        - なので、これ以上細かくしてもほとんどの人は一部しか使わないだろう、と著者らは考えている
        - 例えば100点満点で点数をつけてと言われても人は「これは60点、こっちは80点」みたいに粗い使い方をする
    - 偶数であることの意味
        - 「どちらでもない」みたいなニュートラルな評価がないことで「あえて言えば良いのか悪いのか」を表明することになり、差が出やすくなる、と著者らは考えている
        - これは実験的に良し悪しが検証されたものではなく、単なる著者らの解釈
        - ニュートラルな選択肢がないことによって、本当はニュートラルな気持ちの人が気持ちを正確に表現できず、良いか悪いかを無理やり捻り出すことになってしまいメッセージを歪めてる、という解釈もできる
        - 「候補から一つ選んで多数決」の酷さに比べるとこの件の歪みは大したもんではないのでどっちでもいいんじゃないかな(西尾の解釈)
        - 後述の「投票の初期値を決める」パターンだとニュートラルな値があった方が都合がいい
    - 2段階にした場合、1970年代に提案された[[是認投票]]([[Approval voting]])と同じ構造になる
        - 段階を増やすことによって表現力を増したと解釈できる

ウソのないアンケートとしての機能
- アンケートにウソが混じるなら分析しても意味がない [Tweet](https://twitter.com/absinthe9999999/status/1407881914317373443)
    - > 退職する社員から「社内サーベイは上司から何か言われるのが面倒なので常に最高点を機械的につけていた。辞めることを考え始めてからずっとそうしてきた」と言われ、それを伝え聞いたサーベイ担当者が押し黙ったまま改善策が出てこないMTGで午前が終わりそう。
    - > これが「サーベイの結果からエンゲージメントは下がっていないのに退職するのは何故か問題」の１つの回答なんだけど、担当者からするとなかなか受け入れ難いようだ。
    - >  でもこういうことをするのが[[生身の人間]]だと思うんだよね。
    - > サーベイの設計は匿名式で、上司が直接バイネームで回答者を特定はできないものの、人数が５人以下など少数のチームだと「ネガティブな回答した？理由は何？」などと1on1でメンバー全員が聞かれるといった事態が発生しており、匿名式だから皆が正直に答えるかは微妙。。。
- 正直に答えることが損になる=ウソをつくことによって得をする=耐戦略性がない
- 耐戦略性のないメカニズムで収集されたデータを分析しても、値の分布がそもそも真の分布からズレてるから解釈が難しい
- Majorty Judgementの投票結果は、各選択肢の6段階評価アンケートとしても使える
    - ウソの入ってない質の良いデータ
    - ただしなんでも聞きたいことが聞けるわけではない
- Q: この例は投票の情報が上司に漏れることによって正直に投票しないインセンティブになってたわけだが、情報が漏れる場合はMJでも同じでは？
    - A: もちろんそう。加えて、たとえ情報が一切もれなくても、答えることでメリットが得られないなら「真面目に考えるだけ労力の損」だからやっぱり真面目に答えない
        - 答えた結果によって組織内のリソース分配が変わるなどの理由で真面目に答えるインセンティブがあることが大前提で、それに加えて耐戦略性のある方法を使えばそこで集まったデータは歪みのないアンケート結果にもなる、という感じ

一旦まとめ
- 複数人の意見を持ち寄って意思決定をするメカニズムに関して、伝統的に「一番いいと思う候補に投票して、票が一番多かったものにする」という多数決が使われがち
    - これは票割れの問題がある
    - ウソをつくと有利になるメカニズムでもある
- 「各選択肢を6段階評価し、中央値の最も高いものを選ぶ」というMajorty Judgementのメカニズムが紹介された
    - これは票割れの問題がない
    - ウソをつくことが有利にならない(後述)
- ウソの混ざったデータは役に立たない
    - MJにはウソの混ざらないアンケートとしての機能もある

耐戦略性
- ここからだんだん数学
- MJで「ウソをつくことが有利にならない」とはどういうことか
- 自分の評価がMJによって決定される社会的評価よりも高い時に、ウソをついても社会的評価を釣り上げることができない
    - ![image](https://gyazo.com/71033fdd8b9ce54b2e6f8f1d5acbc34e/thumb/1000)
- 逆も同様で、社会的評価を引きずり下ろすこともできない
- 「自分が社会的評価よりも高く評価してる時に、ウソをついて社会的評価を下げること」はできる
    - でもそれは自分にとって損だからやらない

    - ![image](https://gyazo.com/9710b18fe00f83ffdfc348f95c6f65b9/thumb/1000)
- これは順位関数が一般的に持つ特徴
- 順位関数だけか？
    - 評価語彙を実数の区間とし、集約関数の連続性を仮定するなら、順位関数のみが耐戦略性と、匿名性、一致性、単調性を満たす唯一の関数である
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>数学的には定理が証明できたことに価値があるんだろうけど、現実的には評価語彙が実数の区間ってのは考えにくいし、評価語彙が有限集合である場合には順位関数以外の例を作れるので、あんまりグッとこない🤔
- 順位関数が色々ある中でなぜ中央値関数を使うのか
    - 過半数の評価が一致してrであるときに社会的評価もrである性質がある
    - これを持つのが中央値関数だけ
    - 投票者の不満を「自分の評価と社会的評価の乖離」と定義して最小化をした場合もやはり中央値関数になる
- この辺りの話を数学的にきちんと追いたければ「1人1票からMajority Judgmentへ」 [PDF](http://www.orsj.or.jp/archive2/or57-06/or57_6_295.pdf)が良い解説

[[ボルダルール]]との関連
- ボルダルールでは投票者は各候補者を順位づけする
    - そして順位の高いものほど高い得点がつくようにし、その得点の合算で勝者を決める
    - [https://ja.m.wikipedia.org/wiki/ボルダ得点](https://ja.m.wikipedia.org/wiki/ボルダ得点)
    - ![image](https://gyazo.com/6419b00fbf2a3d4fde0af56138be74f7/thumb/1000)
- 伝統的な投票の改善案として紹介されることがあるが、耐戦略性という観点では弱い
    - 例えばA〜Eの5人の候補者がいる投票で、まともな候補者はAとBの2人だけで残りは特定民族を虐殺するようなヤバいやつだとする
    - 簡単にするために投票者は3人、二人はA派で一人がB派とする
    - 正直に投票するとAが勝つ
        - ![image](https://gyazo.com/c52d6a383dce63a988a555f33cbac980/thumb/1000)
    - ここでB派の人が「Aは過激派より更に好ましくない」とウソをつくとBが勝つ
        - B派はその方が自分に有利なので嘘をつく
        - ![image](https://gyazo.com/e5157d1f4bc7752bfcc027e9e5872cde/thumb/1000)
    - A派にとってB派だけが戦略的投票をすることでBが勝つのは好ましくない
        - そこでA派も同じように「Bは過激派よりさらに悪い」と戦略的投票をしたとすると…
        - ![image](https://gyazo.com/920c5f66b708aee0522f92f23b819ce4/thumb/1000)
        - なんとまともな候補者が足を引っ張りあって誰も望んでない過激派が勝ってしまった！
- ボルダルールとMajorty Judgementを比較した場合
    - N候補者を同じ値禁止でN段階評価したものがボルダ得点に相当する
    - ボルダルールではこれの和を取り、MJでは中央値を取る
    - 要するに[[平均値が外れ値の影響を受ける現象]]の一種
    - 集計方法を中央値にしたらさっきB派の人が「Aは過激派より更に好ましくない」とウソをつく攻撃は成立しなくなる
        - 5,5,1の中央値も5だから
        - ![image](https://gyazo.com/98b8b8fdeece4402f4b2335ed43c0c43/thumb/1000)

kintoneで作ってみる
- ![image](https://gyazo.com/76d0cbf4f097adfef0a617c56917b5c7/thumb/1000)
- ![image](https://gyazo.com/a8dd4a46c198bd46de65b223f1e224f7/thumb/1000)
- ![image](https://gyazo.com/b1f60667d7b764255a3afd26c57a5124/thumb/1000)
- レコード数で集計して、ソートを「集計値」ではなく昇順や降順にする
    - そうすると円グラフの6時の位置が中央値になる
    - ラジオボタンの選択肢の頭に数を入れるのがコツと思ったが違った
        - ソートは選択肢の並び順だから昇順で6が先に来る
        - 先頭に数字を入れたのは関係ない
- 複数の選択肢についてそれぞれ集計するのもできると思う
    - できた
        - ![image](https://gyazo.com/1c753d70f5991245592b218e234f7508/thumb/1000)
            - 凡例の並び順と積み上げグラフの色の順が逆なのが気持ち悪いが…
            - 配色はヒートマップ的にグラデーションにした方が見栄えがいいかも
    - 50%のラインを見て判断すれば良い
        - この場合は50%ラインが両方「どちらかと言えば良い」なので「中央値以上の票数」が多いB案の勝ち
            - ![image](https://gyazo.com/c62cce74b55261a79b82755551807737/thumb/1000)
            - 本当はこの順位に基づいて選択肢がソートされるとどれが一位なのかわかりやすくて良いのだがやり方がわからなかった
                - さすがにJSカスタマイズを使わないとダメかな？
- 複数の選択肢について一人一票に制限する方法がわからなかった
    - 特に「案Aには投票したが案Bには投票しなかった人」がいる場合どうするか
        - 案1: 全部投票した場合だけを有効票とする
            - うっかり見落としで無効票になるのかわいそう
        - 案2: 投票した人の中の中央値にする
            - 上記の実装ではとりあえずそうしたんだけど、この場合になんか戦略操作が可能になったりしないか？
        - 案3: 選択肢を奇数にして、投票なしはニュートラルとする
            - これが確実だよなぁと思う
            - 投票者全員分のレコードを管理者が一括で追加する、ニュートラル投票で。
            - 投票者は好きなタイミングで編集をする。
            - アプリのレコード追加を管理者権限にすれば良い
                - 一般の人は閲覧と更新だけ
                    - ![image](https://gyazo.com/380806f458ab5b045ebc85fb96bf72b2/thumb/1000)
                - さらにレコード閲覧権限を自分が投票者に指名されてるレコードだけにすれば他人の投票は閲覧できない
        - 案4:  一つのレコードに入れて全部必須回答にすれば、部分的に投票された状態は発生しない
- 耐戦略性があれば途中結果を公開しても大丈夫か？
    - せっかくkintoneで集計が見られるならリアルタイムで「現在のみんなの気持ち」が可視化されてた方が面白げ
        - それを見て更に議論が盛り上がるかも？
        - 議論を聞いて投票を変更してもいい？
            - 「最初はA案をとても良いって考えてたけど、批判の意見を聞いて気持ちが変わった」的なもの
- 投票が行われてることは投票権を持つ人すべてに伝えられていることが前提

アローの不可能性定理との関係
- Q: [[アローの不可能性定理]]から、性質の良い投票は不可能だと証明済では？
- A: その定理は投票者が選好をメッセージとして出すモデル
    - 「候補Bは候補Cより好ましく、候補Cは候補Aより好ましい」的なやつ
        - MJはそうではない。各候補の好ましさを順序尺度(例えば6段階評価の値や、0〜100の実数)で表現するもの
        - この尺度の意味が投票者の間で共有されてることが前提。6段階評価程度ならおおよそ現実的な仮定だと思う
    - 「候補Bは候補Cより好ましく、候補Cは候補Aより好ましい」には、CがBとギリギリ負けるぐらい良いのか、全然良くなくてAにギリギリ勝つぐらい悪いのかの情報がない
        - MJの方法はより多くの情報を集められる
    - アローの「無関係な候補からの独立性」が強すぎる要請だという主張もある
- そもそもアローの不可能性定理は耐戦略性の話ではない
    - 耐戦略性が絡むのは[[ギバート＝サタスウェイト定理]]の方
    - こちらも選好をメッセージとするメカニズム

発表後の議論
- 多数決に色々なパターンがある話
- [[多数決を疑う]]
    - 色々なスコアリングルールを比較している
        - ![image](https://gyazo.com/44c42ffb3439544d86a1b14476bfa95a/thumb/1000)![image](https://gyazo.com/1b9a369478ed10a577152aac2809db29/thumb/1000)
            - p.58-59
- 実はこの本の著者[[坂井 豊貴]]は前回の[[メカニズムデザイン勉強会]]で紹介した2冊の参考図書の著者でもある
    - 2008 [[メカニズムデザイン(書籍)]]
    - 2015 [[多数決を疑う]]
    - 2016 [多数決の代替案として最適な「ボルダルール」 | 「決め方」の経済学 | ダイヤモンド・オンライン](https://diamond.jp/articles/-/96679)
        - > 多数決には、「票の割れ」という致命的な欠陥があるため、多数派の意見さえ反映されない...そのため、『「決め方」の経済学』の著者である坂井豊貴氏は、「ボルダルール」という方法を代替案として提案する。なぜなら、「満場一致に最も近い方法」だからだ。
    - 2019 [Twitter](https://twitter.com/toyotaka_sakai/status/1166885111838593024)
        - > 明日の Auction Lab で扱う Majority Judgment（MJ）について。実際に使ってみると、学ぶものがめちゃくちゃありました。MJはすごいです。僕はこれまで社会的選択理論は「選挙制度」「世論調査方式」に使うものと捉えていたのですが、ビジネスに活用できますね。
    - 2020 [[メカニズムデザインで勝つ]]
- 質問してみたら回答いただけた
    - > nishio: 先生の2015「多数決を疑う」2016「多数決の代替案として最適なボルダルール」(ダイヤモンドオンライン)と2020「メカニズムデザインで勝つ」を拝見しました。
        - >  今でも多数決の代替案としてボルダルールが最適だと思いますか？それともMajority Judgementが良いと思いますか？
    - > [toyotaka_sakai](https://twitter.com/toyotaka_sakai/status/1415316449531359242): 選択肢が増えるにつれ、ボルダは「各人の１位と２位」の差（の結果への影響）がゼロに収束することを、よくないように感じます。理論家としては、それがどういう意味で「よくない」かは明瞭にすべきですし、「感じます」は定理の形にすべきです。が、やっていません。
        - > 戦略的操作の観点からは、MJはボルダよりずっとよいです。だからMJとボルダどちらかを選べと言われたら、MJでしょうか。なぜ私が以前はそんなにMJを評価してなかったかというと、MJは非常に変わっていて、伝統的なArrovian Social Choiceの枠組みで記述できないから。受け入れるのに時間がかかった。
        - > ただしボルダルールの美点は、「一位に３点、二位に２点、三位に１点を配点するボルダルール」と言葉だけで１０秒以内に伝えられるところ。ラジオでも新聞でも伝えられる。MJはラジオも新聞でも伝えられません。MJは動画だと伝えられますが、私がフリップを用いた説明に使える時間が１分は要ります。
    - > nishio: ご回答ありがとうございます！MJでは投票者のメッセージが伝統的な選好順序よりも情報量の多いものになったところが私個人はとても好きですが、理論上は伝統的なモデルに従わないことが受け入れにくさにつながったわけですね。MJの説明しにくさは、経験者を増やせば時間が解決するかもと思います。

ペア敗者規準
- ペア敗者規準: ペア敗者（候補者の中から 2 人を選んだときに、どのペアでも負ける候補者）を選ばない性質
- 「多数決を疑う」では、ペア敗者規準を満たすのはボルダルールだけ、とされている。
- Q: MJはペア敗者規準を満たすのか？
- A: MJでどのペアでも負けてる候補は中央値が最低の候補だから全体でも当然負ける(=ペア敗者規準を満たす)

---以下メモ
多数決
票の割れ
多数決というネーミング
多数派が幸せになりそうだがそうではない

5〜7段階
何段階にするかは重要ではない
2段階にしたものを是認投票という
歴史的には1970年に是認投票が研究されていて、それの改良版がMJ

タイブレーク
- 中央値以上の票数で決める

過激な意見
周囲に似た意見の候補者がいないので票を集めやすい

中央値
- 戦略的操作に強い
- 外れ値の影響を受けにくいから

ウソの入ったデータには価値がない

理想的な投票方式は存在しない

フランス大統領選
[[ウソとは何か]]


[Majority judgment - Wikipedia](https://en.wikipedia.org/wiki/Majority_judgment)

[Tactical voting - Wikipedia](https://en.wikipedia.org/wiki/Tactical_voting)


1人1票からMajority Judgmentへ [PDF](http://www.orsj.or.jp/archive2/or57-06/or57_6_295.pdf)
- > 従来の 1 人 1 票の投票や，個人の選好順序を前提にして社会的選択を行うことの問題点が認識されて久しいが，近年 Balinski と Laraki はその問題点を克服する方法として Majority Judgment と名付けられた方法を提案している．この稿はその理論的妥当性についての彼らの議論を紹介する．
キーワード：1 人 1 票，選挙，社会的選択，Majority Judgment，アローの定理，順位関数
- 定義域の非限定性
- 一致性
- 非独裁性
- アローの定理
    - 選択肢が3個以上の時、上記3つを満たす社会的厚生関数は存在しない
- 共通語彙による評価
    - 共通語彙に順序が入っていて、意味が共有されていれば良い
    - 0以上100以下の実数とかでも良い
    - 社会的評価関数
        - 持つべき性質
            - 中立性
            - 無関係対象からの独立性
        - これが満たされるなら集約関数が存在する
    - 集約関数
        - 持つべき性質
            - 匿名性
            - 一致性
            - 単調性
        - 戦略的操作可能性について
            - 戦略的操作
            - 戦略的操作不可能性
        - 順位関数は全部の要請を満たす
            - 順位関数がなぜ戦略的操作不可能性を満たすか
        - 要請を満たす他の関数があるか？
            - 評価語彙を実数の区間とし、集約関数の連続性を仮定するなら、順位関数のみが要請を満たす
        - 動機を持たない評価の操作に関して
            - 社会的評価を上げ下げできる人は多くて1名である
            - 評価を操作できる人は高々1名であり、高々1名であるような集約関数は順位関数のみである
            - 注: 連続性が仮定されてる
                - 語彙が有限集合の場合には他にも条件を満たす集約関数があり得る
    - ではどのような順位がよいか
        - 過半数の評価が一致してrである時に社会的評価もrである性質
            - これを持つのは中央値だけ
        - 自分の評価と社会的評価の乖離を不満に思うとして不満を最小化する集約関数を探すとやっぱり中央値
- 社会実験
    - フランス大統領選の投票者を対象とする実験
    - 候補者は実際の12人
    - 投票を終えて出てきた人を対象に実験へ勧誘
    - 2383人の74%が実験に参加
    - 1733件の有効票
    - 6段階評価にしたが86%が5個しか使わなかったのでこれくらいで十分
    - ほとんどの投票は1分未満
        - ネガティブな投票ができることの満足度が高い


Balinski, M. and Laraki, R., 2007. A theory of measuring, electing, and ranking. Proceedings of the National Academy of Sciences, 104(21), pp.8720-8725.
[PDF](https://www.pnas.org/content/pnas/104/21/8720.full.pdf)
- アローの不可能定理
    - 伝統的な投票モデルでは満足のいく方法は存在しない
- より現実的なモデル
    - LaplaceとGalton由来
    - 不可能性を避ける新しい方法
    - 現実的に実行可能な方法
    - Majority Judgememt
- 社会的選択
    - 複数の個々人の評価を集めて一つの評価にする
    - 2つ応用がある
        - 投票: 例えば複数の候補者から一人選ぶとか、複数の選択肢から一つ選ぶとか
        - Jury Desicion: 例えば審査員がワインの等級を決めたり、フィギュアスケートの競技者の点数を決めたりする
- 社会決定関数SDF
    - 投票者のメッセージを入力とし、勝者または候補者のランキングを返す
    - 色々バリエーションがある
- 伝統的モデル
    - [[コンドルセ]]の方法　1299
    - [[ボルダルール]]　1433
    - 投票者が順序づけをするモデル
    - 順序の意味が曖昧
        - 3通りある
- 現実社会
    - 投票者のメッセージは単にメッセージであり、選好に基づいているがそれ自身ではない
- [[アローの不可能性定理]]
    - 投票者が選好を表明するという伝統的モデルに基づいて
    - 3つの基本的な特徴を兼ね備えた社会更生関数SWFが存在しないことを示した
        - 選択肢が2件の場合を除く
    - [[アマルティア・セン]]
        - 投票者が実数値を入力するモデル
        - 選好ではなく効用
        - 興味深いが実用的でない、効用が複雑な概念
        - アローの不可能定理が再現
            - 効用が比較可能でない限り
        - このモデルは[[ギバート＝サタスウェイト定理]]の証明に用いられた
            - 投票者が真の選好を表明することがドミナント戦略になるような社会選択関数はない
    - 出力がrank orderingなら入力はover rank orderingsの選好であるべきでは？
    - いろんな提案
        - Lullの提案　コンドルセ
        - Cusanusの提案　ボルダ
        - approval voting
    - 主張
        - 1: アローおよびその他の不可能性定理は伝統的モデルでは解がないことを示してる
        - 2: 伝統的モデルはそもそも十分にメッセージや目的をモデル化してない
        - 3: 新しいモデルが必要だ
    - 現実の応用が別の入力を示唆してる
        - オリンピックのフィギュアスケートとか、ワインの格付け
        - ケルビン
        - 投票と市場
            - お金で表現
    - 共通言語
        - ワインを個人的に好んでも低いグレードをつけることがある
        - つまりインプットは選好ではなく共通言語による格付けである
        - アローの不可能定理は共通言語の不在によって起きている
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この「共通言語」のあたり、既存のモデルとの違いをきわだてるためにこういう書き方をしてて、逆に「共通言語なんて無理では？」みたいな気持ちになる人がいそう
        - もし仮に100点満点でのランキングをしてて、みんなが40〜60を使ってるのにAさんが80〜100で出力したとしたら何が起こるか
        - Aさんのメッセージは全部1位になって、中央値を1つ引っ張り上げる効果だけになる
        - つまり共通言語から離れたメッセージは単に情報量が下がるだけ
        - 現実的には共通言語っていっても6段階評価とかなのでそれほど深刻な差は発生しないだろう



[https://www.kyoto-su.ac.jp/graduate/tsushin/t_ec/econ-journal/ronbun/pdf/ronbun07_04.pdf](https://www.kyoto-su.ac.jp/graduate/tsushin/t_ec/econ-journal/ronbun/pdf/ronbun07_04.pdf)




集約関数の特徴づけ [PDF](https://www.bunkyo.ac.jp/faculty/business/feature/journal/pdf/vol3/business_journal_vol3_02.pdf)
- > 本稿では Balinski と Laraki によっ提案された Majority Judgment で中心的な役割を演じる集約関数の問題点を指摘し、それが強単調性の条件を緩めることによって解消できることを示す。さらに評価者の評価が大きく割れた場合の社会的評価が集約関数を一意的に決定することを示す。
