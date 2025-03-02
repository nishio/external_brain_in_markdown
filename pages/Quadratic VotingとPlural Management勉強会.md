---
title: "Quadratic VotingとPlural Management勉強会"
---

[[Quadratic Voting]](QV)と[[Plural Management Protocol]](PMP)勉強会
- 2024-03-15 [[サイボウズラボ勉強会]]
- 前回[[Plural Management勉強会]]で出来立てホヤホヤの"Plural Management"論文を読んだ
    - > South, Tobin and Erichsen, Leon and Jain, Shrey and Maymounkov, Petar and Moore, Scott and Weyl, Eric Glen, [[Plural Management]] (January 9, 2024)
- その結果、[[Quadratic Voting]]から説明すべきだと気づいた
- 今回の話は下記の二つ
    - [[Quadratic Voting]]
        - > [[Quadratic Voting: How Mechanism Design Can Radicalize Democracy]]
        - > Steven Lalley, E. Glen Weyl (2012~2018)
    - [[Quadratic Funding]]
        - > [[Liberal Radicalism: A Flexible Design For Philanthropic Matching Funds]]
        - > Buterin, Vitalik and Hitzig, Zoë and Weyl, Eric Glen (2018)
    - 余裕があれば[[Plural Management]]の話
- 関連
    - これって[[メカニズムデザイン]]の話
        - [[メカニズムデザイン勉強会]]/[[Majority Judgement勉強会]](2021にやった)
        - この時にMajority Judgement(2007)の説明をした
        - [[一人一票が不自然]] by [[坂井 豊貴]](メカニズムデザイン勉強会で読んだ本の著者のQVに対する言及)

Quadratic Voting
- 参加者が「意見の強さ」を表現できるように設計された投票システム
- 和書では[[ラディカル・マーケット]]とかで解説されてる
    - 原著: Radical Markets: Uprooting Capitalism and Democracy for a Just Society
        - [[Eric A. Posner]], [[E. Glen Weyl]](2018)
- 「意見の強さをを表現できるようにしよう」って言うと、素朴に思いつくのは5段階投票
    - 「強い賛成」「弱い賛成」「中立」「弱い反対」「強い反対」の5段階にする
- これだと何がダメなの？
- 「強い賛成」と「弱い賛成」のコストが同じなので、文化によっては「弱い主張の存在する意味がわからん」となる
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>5段階評価をしたときに文化によって投票の分布が異なることを解説して
    - <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>文化的謙虚さと自己表現
        - 高コンテキスト文化（アジアの国々など）では、人々はしばしば[[謙虚さ]]を重んじ、自己の成果や満足を控えめに表現する傾向があります。これは、5段階評価で極端に高いまたは低い評価を避け、中間の選択肢を好む傾向に反映されることがあります。
        - 低コンテキスト文化（アメリカや西ヨーロッパの国々など）では、[[個人主義]]が強調され、自己の意見や成果をはっきりと表現することが奨励されます。これは、より極端な評価（「1」または「5」）を行う傾向につながることがあります。
    - ![image](https://gyazo.com/196b0f1254fb49486d2291d5e1eab25b/thumb/1000)
        - [[ラディカル・マーケット]] p.175~176
            - > [[リッカート調査]]は回答者に選好の強さを正直に示すように強制するものではないため回答者は大げさに言う傾向がある
        - これは低コンテキスト文化のアメリカの話
- では、強い主張ほど高いコストが掛かるようにしよう！
    - →どのようなコスト関数が適切か？
- [[Quadratic Voting: How Mechanism Design Can Radicalize Democracy]]
    - preprint(2012)
    - > [[メカニズムデザイン]]は[[民主主義]]を救えるか？私たちは機会を提供するシンプルな設計を提案します：個々の人々が希望するだけの投票権を与えますが、そのコストは購入した投票権の数の二次関数に比例します。二次関数的コストのみが、購入した投票についての限界費用を線形にし、したがって個々の人々の投票の評価が結果の変更の価値に比例し、福祉最適性をもたらします。さまざまな分析と証拠が示すところでは、このまだ発展途上の機構が既存の民主主義の失敗を強固に修正し、選好の強度と知識を組み込むことができるという大きな約束があります。
- 二次関数的コストがいい
    - <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Quadratic Votingの主なアイデアは、各参加者が複数の票を購入し、自分が支持する選択肢に投票できることですが、投じる票の数が増えるごとに、そのコストは二次関数的に増加します。つまり、1票目は1単位のコストがかかりますが、2票目を得るには追加で3単位（合計4単位）、3票目を得るにはさらに5単位（合計9単位）のコストがかかります。
    - これがQuadratic Voting
- なぜ二次関数的コストがいいのか
    - 以前[[Quadratic Votingはなぜ平方根を取るのか]]で少し解説した、それをここで整理する
    - 2012の段階では少し強い仮定をおいて計算している
        - そんな仮定をおいていいの？となる
    - 2014に"[[Nash Equilbria for Quadratic Voting]]"で、強い仮定をおかなくても理想との差がO(1/N)になることが示される
        - が、この証明には[[ベイジアンナッシュ均衡]]を使うのでここでは解説しない
        - ここではラフな解説で雰囲気を伝える

なぜ二次関数的コストがいいのか
- ![image](https://gyazo.com/78edad99698c1844d5808c5a95d3339e/thumb/1000)
- AかBかを選ぶ二択投票を考える
- 1 person 1 vote([[一人一票]])の投票メカニズムでは投票者は+1か-1の投票をする($v_i \in \{-1, +1\}$)
    - それを足し合わせたもの$\sum_i v_i$が0より大きければAの勝ち
- でも人によって「どれくらい強くその結果を望んでいるのか」$u_i$は異なる
    - 投票者は+1か-1の投票しかできない($v_i \in \{-1, +1\}$)
    - その結果「Aであることがとても大事なんだ！」($u_i = +10$)の人と「どっちでもいいけど、どっちかといったらBかな〜」($u_i = -1$)の人の投票が同じ力を持ち相殺する
    - これはよくないね！
        - 2番の人と同じ選好の人がもう一人居たら、[[一人一票]]の投票メカニズムではBに決まってしまう
            - その場合のそれぞれの人の効用は(-10, +1, +1)
        - Aに決めれば(+10, -1, -1)だったので、こっちの方がみんなの効用の和が大きい
            - 一人一票の投票メカニズムでは少数派が大損する選択肢が選ばれてしまう
                - [[多数派の専制]] by [[アレクシ・ド・トクヴィル]]
                - [[彼らが最初共産主義者を攻撃したとき]] by [[マルテイン・ニーメラー]]
        - みんなの効用の和: $\sum_i u_i$によって決めたい
- そこで「どれくらい強くその結果を望んでいるのか」$u_i$を投票者に表明させることにする
    - しかし素朴に「どれくらい強い？」と聞いたら大きい数を答えた方が自分の望む結果になる確率が高まるのでみんな上限いっぱいの強さを主張して実質[[一人一票]]になってしまう
    - だから「強さ」を大きくすることに対してコスト$c(v_i)$の支払いを要求する
    - このコスト関数$c$をどう設計するのが「良い」かなというのがこの論文のトピック
- まず「良さ」を定義する必要がある
    - robustly optimal:
        - $ \sum v_i$ と $ \sum u_i$ が同じ符号であること
    - つまり票数を足し合わせた場合の判断結果と、「気持ちの強さ」を足し合わせた場合の判断結果が一致すること
- Mueller (1973) と Laine (1977)が提案したmarginal pivotality $p$に全員同意しているとする
    - 1票入れた時の結果が変わる確率
    - この仮定はかなり強い仮定
- この場合の合理的な投票数は$2u_i pv_i − c (v_i)$を最大化するものになる
    - 2はcの係数部分で吸収されるのでどうでもいいが、結果Aの効用が$+u_i$でBの効用が$-u_i$としてるから2倍になる
    - pは「1票あたりのpivotality」なので$pv_i$がpivotalityになり、$u_i$を掛けることで期待効用になる
    - 個々人は期待効用からコストを引いたものを最大化する
- cが二次関数である場合に限りrobustly optimalになる
    - 証明は別紙で展開されていて、本文では簡単に要約している
    - 簡単に言えば
        - $2u_i pv_i − c (v_i)$が最大化されているのだから$v$で微分すれば0になる
        - $2pu_i = c(v_i)'$が成り立つ
        - robustly optimalであるためには$u_i \propto v_i$(比例する)のが都合がいい
        - そうなるのは$c$が二次関数の時だけ
- ちなみに素朴な「1票1ドル」だとどうなるか
    - 一番効用の高い人が十分な票を買って、その人の意思で結果が決まる
    - 商品取引としてみればオークション、意思決定としてみれば独裁制
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q: 「[[心を動かす]]」(共感を引き出して仲間を増やす行動)は従来型の民主主義のためのものなのかな
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A: 違います。Quadratic Votingでも、1人で10票入れるのには100コストが掛かりますが、仲間を増やして10人で1票ずつ入れれば10コストで10票入れられます。より大勢の人に理解してもらうことにインセンティブがあります。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. コストが2乗でも、イーロン・マスクが全部買い占めて、みたいなことにはならない？
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. 買い占めるのに2乗のコストがかかるだけです。イーロン・マスクはそれをしたくて、それくらい出すのであれば、それは好ましい。
        - 補足説明: 「買い占め」を「一人で多数派になる」と解釈して回答した、票数に上限はないので商品の買い占めに相当することは起こらない
        - 1票100円で、1万人で投票をして、マスク以外全員がAに投票してる場合、マスクは100億円払って1万票を買ってBに投票することで一人でBに決定することができる
        - もし人々がBに決まることを好ましくないと思うのであれば、もう100円出してAに投票すれば良い。人々が200円払うなら、マスクは200億円払う必要がある
        - 人々が追加で100円払う価値を見出さないのであれば人々にとってこのテーマはそれほど重要ではなくBに決まっても構わない、AかBかは100円以下の価値しかないということ。だからマスクの一存でBに決まることは正しいこと。「特に興味のない大勢」によって「強い興味のある少数派」の足が引っ張られる「多数派の専制」を防げている。
        - なおこの時、マスクの払った100億円によって国庫に一人当たり100万円のプラスがある。100円程度の価値もない意思決定において譲ることの対価として十分大きい。
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. 個人が買い占めのコストを掛けてもやりたいなら、社会的にはそれも正解、という考え方ってっことかな
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. その人がそれだけ強く望んでいるなら、少数派の意思を多数派が99%で押しつぶすよりは、それだけ強く望んでいる人の意思を尊重する方が良いというのがQuadratic Votingの主張です。良さの定義がrobustly optimal: 「票数を足し合わせた場合の判断結果と、気持ちの強さを足し合わせた場合の判断結果が一致すること」
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>コスト配分の偏りはない、みたいな仮定がないと民主的な感じはしない
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>お金を使った場合は、1ドルの重みが人によって異なることはある。お金を使うことはQVの必要条件ではないので、それが問題だと思うのであればお金でないトークンを民主的に配布すれば良い。実際そうやってる例が多いので応用例を見てみよう。

Quadratic Votingの応用事例<img src='https://scrapbox.io/api/pages/nishio/pplx/icon' alt='pplx.icon' height="19.5"/>
- 政治的意思決定(2019)
    - 2019年4月にコロラド州下院の民主党幹部会による実験でQVが実施されました。議員たちは、今後2年間の立法上の優先事項を決定するためにこれを使用し、107の法案の中から選択しました。...政府の透明性を促進するためのオープンソースの[[液体民主主義]]プラットフォームである[[Democracy Earth]]によって提供されました。 --- [Quadratic voting - Wikipedia](https://en.wikipedia.org/wiki/Quadratic_voting)
- 総統杯ハッカソン投票(2019): 台湾では、台北の[[RadicalxChange]]が主催した総統杯ハッカソンイベントで、QVが適用された。
- 公的予算の配分: 台湾政府が運営するe-デモクラシー・プラットフォーム「[[Join]]」では、予算に関する市民参加を促進するためにQVが用いられている。
- etc...
- ざっくり「使われ始めて5年くらい経った」という状況

アローの不可能性定理
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>アローの不可能性定理は集団的意思決定の文脈で、任意の投票ルールが満たすべきと考えられるいくつかの公理（例えば、非独裁、パレート効率性、独立性など）を全て満たすことは不可能であるという理論です。これは、従来の投票システムが複雑な社会的選好を公平かつ効率的に反映することに限界があることを意味します。Quadratic Votingはこの問題に対する一つの解決策を提供します。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>良い性質を持った投票システムが不可能！
- ↑これは誤った[[過度の一般化]]
- 一般人が「投票」という言葉でイメージするものの、ここでアローが扱っているものは違う
- アローの不可能性定理は「どんな選好投票システムも〜の条件を同時に満たすことはできない」
    - 選好投票とは
    - <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>選好投票（[[preference voting]], [[ranked voting]]）は、投票者が選挙や決定事項における複数の選択肢に対する自身の[[選好順序]]を表現する投票方法です。この方式では、投票者は最も好ましいと思われる選択肢から順に、全ての選択肢をランク付けします。選好投票は、選択肢間の相対的な好みをより詳細に反映できるため、多くの場合、より情報豊かな選挙結果をもたらします。
- 以前[[Majority Judgement勉強会]]のときは、Majority Judgementが選択肢の「選好順序」ではなく「絶対評価」を投票するので、不可能性定理の対象ではないという話をした
- 今回のQuadratic Votingも同様に選択肢の「選好順序」ではなく「絶対評価」を投票するシステム(少なくともオリジナルの発想では)

継続価値
- 「少なくともオリジナルの発想では」という留保の理由
- > As is common in the analysis of markets for private goods (Willig, 1976), we assume there are enough issues and that each is sufficiently inconsequential that every voter has a quasi-linear “continuation value” for retaining voice credits for future votes.
    - <img src='https://scrapbox.io/api/pages/nishio/GPT-4/icon' alt='GPT-4.icon' height="19.5"/>私的財の市場分析で一般的なように（Willig, 1976）、問題が十分に多く、それぞれが十分に無関係であるため、すべての投票者は将来の投票のために発言権クレジットを保持する「[[継続価値]]」を持っていると仮定します。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>今の一般的な投票においては投票権は「その時に行使しなければ価値を失うトークン」なわけだが、この論文における「[[発言権クレジット]]」は将来の投票のために「取っておくこと」ができる
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>QVに継続価値を用いるものと用いないものがあるよね
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>はい、Quadratic Voting（二次投票）を使用する場合、継続価値（キャリーオーバー）を利用するシステムと利用しないシステムがあります。
    - 継続価値を利用する場合、参加者は一定期間内に使用しなかった投票権（またはその価値）を次の期間に持ち越すことができます。これにより、参加者は将来の投票でより大きな影響を持たせたい場合に、資源を節約する戦略をとることができます。
    - 一方、継続価値を利用しないシステムでは、各投票期間が独立しており、未使用の投票権は失われます。これはシンプルで直接的なアプローチですが、参加者には各投票期間内でのみ戦略を練るインセンティブが与えられます。
- 例えば台湾総統杯ハッカソンの投票では、投票者に99票の投票クレジットを配る
    - こういうタイプの投票は[RxC QV](https://quadraticvote.radicalxchange.org/)ですぐ試せる
- この方法は手軽だが「もらった99票を使い切らないともったいないな」と思う気持ちによって、たいして価値を見出していないものに対しても投票してしまう
    - (継続価値のある)[[QVは投票しないことに意味のあるメカニズム]]
- 一方でクレジットの持ち越しができる場合「良い投票対象がないから取っておこう」ができる
    - この方が投票者の真の選好強度の表明に近い
    - だけど、継続的なアカウント管理とかが必要になって導入が大変

Quadratic Funding
- > [[Liberal Radicalism: A Flexible Design For Philanthropic Matching Funds]]
- > Buterin, [[Vitalik]] and Hitzig, Zoë and Weyl, Eric Glen (2018)
- > (abst)私たちは、慈善的/公的な資金提供に対する設計を提案します。これにより、分散化された自己組織化型の公共財の生態系が（ほぼ）最適な状態で提供されるようにします。この概念はQVのアイデアを、内生的なコミュニティ形成のための資金調達メカニズムに拡張します。市民は彼らにとって価値のあるプロジェクトに募金を行います。プロジェクトが受け取る金額は、受け取った募金の平方根の合計の二乗に比例します。この「標準モデル」では、これが最適な公共財の提供をもたらします。変形はコストを制限し、共謀に対する保護を助け、調整を支援することができます。キャンペーン資金、オープンソースソフトウェアエコシステム、ニュースメディアの資金、都市の公共プロジェクトへの適用について議論します。さらに広く、私たちのメカニズムを政治理論に関連付け、この公共財問題への解決策が、中立で独裁的でない社会のルールを提供し、それでいて集団組織を支援する可能性があるかについて議論します。
- 要するに通貨でQVするわけ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- ボイスクレジットの継続価値をシステムとして実装するのではなく、すでに存在する「継続価値のあるクレジット」である通貨に任せてしまう

Gitcoin
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Quadratic Funding (QF)の応用事例として、[[Gitcoin]]が特に注目されています。
    - Gitcoinは、オープンソースプロジェクトやその他の公共財への資金提供にQFを使用しています。QFは、プロジェクトへの小さな寄付が多数ある場合に、それらをマッチングファンドを用いて増幅させる仕組みです。これにより、より多くの人から支持されるプロジェクトがより多くの資金を受け取ることができ、コミュニティにとって価値の高いプロジェクトへの投資が促進されます​​​​​​。
    - 例えば、Gitcoin Grantsでは、ブロックチェーンプロジェクトの第9ラウンドの資金調達で、12,000人以上のコントリビューターから合計138万ドルが812の異なるプロジェクトに寄付されました。このプラットフォームは、プロジェクトが受け取るマッチングファンドの量を、少額の寄付を行った人数に基づいて決定します。この方式により、小規模または新興のプロジェクトが、大口の寄付に頼らずに資金を調達する機会が増えます​​。
- 全体では50 million USD以上を分配してきてるので日本円で言えば75億円以上
- 規模感を見るために"OSS 寄付"で検索したら見覚えのある会社がトップだった
    - [OSSへの寄付のススメ ~ サイボウズのOSSへの寄付戦略 - Cybozu Inside Out | サイボウズエンジニアのブログ](https://blog.cybozu.io/entry/2022/06/17/150207)
        - > 寄付の総額は現在は売り上げの0.05%にしています。なぜ利益ではなく売り上げなのかというと、利益が出ているかどうかにかかわらずOSSを使っていることには変わりがないので、利益よりも売り上げをベースとしました。
    - [サイボウズ、「kintone」の売上高が100億円突破――今後は中長期的な投資へ - クラウド Watch](https://cloud.watch.impress.co.jp/docs/news/1481021.html)
        - > 2022年の連結売上高は前年比19.4％増の220億6700万円
        - 最近のデータの何が公開可能か調べるのが面倒だったので適当
    - Gitcoinはざっくりサイボウズ700社分の再分配をしている
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>QV/QFは技術によって社会的問題を解決しようとする試みの重要なパーツなのは間違いない

Plural Management Protocol
- 前回での話: [[Plural Management勉強会]]
- > 階層的な組織の権威を、ネットワーク化された権威を可能にするPluralなメカニズムに部分的に置き換えるモデルである「Plural Management」を紹介する。参加者は、組織の優先順位を予測し、それを達成することによって影響力を獲得し、この影響力を利用して優先順位を設定し、貢献を検証することで、ダイナミックで実力ベースの権力構造を育成する。オープンソースソフトウェア開発を例に説明するこのアプローチは、階層的な隘路を必要とすることなく、価値ある貢献と勤勉さを強調し、それによって参加を強化し、適応的な集合知を可能にする。
- > キーワード：マネジメント、Plurality、二次的メカニズム、オープンソース、ソフトウェアマネジメント、組織力学
- ![image](https://gyazo.com/f1adcb67a3ac4116d16d0425c7ebd729/thumb/1000)
- > 組織のメンバーは、仕事を通じてマネジメント・クレジットを動的に獲得することができる。イシュー・ボードでは、クレジットを使った[[Quadratic Funding]]によって、メンバーが課題に優先順位をつけることができる。これらのクレジットは、これらの課題に貢献したメンバーに支払われる。支払いは、権限を行使するためにマネジメント・クレジットを消費する他のメンバーによって行われる二次投票の後にのみ行われる。
- >  組織の管理者は、投票結果を正しく予測したり、貢献に対するデューデリジェンスで個人に報酬を与えたり、既存の管理者の好みを予測したりすることで、メンバーが管理クレジットを獲得できるようにすることを選択できる。
- >  このプロトコルは、単純化された階層を持たない小さなメンバーの集まりから大きな組織までスケールするメカニズムを通じて、ダイナミックな管理制御を可能にする。
- 前回のやり取り
    - > <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>なんで二乗にしたんだろう。いろいろチューニングできそうな項目だなあ。
    - > <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>それが[[Quadratic Voting]]
    - > <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>数学的な根拠があるのか！！
- これを今回説明した

[[Gov4Git]]
- [[Plural Management Protocol]]の実装がGov4git
- それを使って[[Pluralitybook]]が管理されてる
    - [https://github.com/pluralitybook/plurality](https://github.com/pluralitybook/plurality)
    - > GlenWeyl: this should be a show and tell
- 前回[[Plural Management勉強会]]をやった1/26には「まだクレジットはもらってない」という状況だった
- 3/14現在
    - ![image](https://gyazo.com/95fbbf520e911fbe17bfc8eb9082966e/thumb/1000)![image](https://gyazo.com/f4151b037a85c47fbd64622a3382f950/thumb/1000)
    - [Gov4Git community dashboard · Issue #263 · pluralitybook/plurality](https://github.com/pluralitybook/plurality/issues/263)
        - ここで詳細データが見れる
        - ![image](https://gyazo.com/29332ba1f6dc173fa8d028a85a83e44f/thumb/1000)
- 現時点で体験してみてどうだったか
- クレジットで優先順位づけされたissuesを眺めて、貢献できそうなものを探すのは少し面白い
    - インセンティブによって動機づけされて、コミュニティにとって好ましい行動が誘導されてるのを感じる
        - この状態に比べると「コミュニティのissuesを読みもせずに、自分のやりたい実装をやって、いきなりPull Requestする」という感じのムーブは「限られた公共財である"レビューのエネルギー"を個人が消費しようとする行為」だよなぁと感じる
        - OSSプロジェクトが[[共有地の悲劇]]に陥らないためにメカニズムでなんとかしよう、という方向に一歩進んでる感はある
- 貢献自体はGithub単体でも検証可能であった、その貢献がコミュニティからどう評価されているかが検証不可能だった、個々人の心の中の値になっていた、それがクレジットとして可視化されるようになった
    - ![image](https://gyazo.com/839a476c8d02d070eb97787dfaa21805/thumb/1000)
        - 過剰に詳細
        - 多分今のGithubでコンパクトに示せるのはこれ
            - ![image](https://gyazo.com/af8b72f00f15905925e69421643e08d6/thumb/1000)
- 現状はまだゲームのチュートリアルの状態だと感じる、本編が開始してない
    - 僕のような一般参加者が建てたissuesはGov4Git管理にならない
        - ![image](https://gyazo.com/265aff1817b1e1051ef2f641002b016c/thumb/1000)
        - gov4gitタグがつかない、つける権限がない、多分Glenがやっている
        - OSSプロジェクトの初期に[[慈悲深い独裁者]]が統治することは正しい
    - プルリクを受け付けるかの判断もGlenがやっていると思う
        - PMPの論文では予測市場を使ってコミュニティが判断という話だったがまだそれは行われてない
        - 正直3/17に原稿FIXをしようとしている今の局面が一番Pull Requestがくるときだと思うので、ここで一人で回ってるならコミュニティで判断する必要はないのではとも思う
    - CreditのIssue
        - ![image](https://gyazo.com/f53f4833228a3ae4bc0a0b7a64e24d0d/thumb/1000)
        - TransferがほとんどなくてIssueされてる
        - 具体例
        - [Issuing credits to Nishio · Issue #407 · pluralitybook/plurality](https://github.com/pluralitybook/plurality/issues/407)
        - ![image](https://gyazo.com/1fa07a34d20d8b86fc69689a5cddd048/thumb/1000)
        - Glenが僕に160000というキリのいい額のcreditをを発行してる
        - これはQFによる分配ではなく管理者コマンドで直接クレジットを発行してると思う
    - というわけで、まだ論文に書かれていた機能のほとんどは体験できていない
        - 一応貢献は認められて投票権を持ってる状態になったので、舞台を観客席からではなく出演人物として観察できる立場にはなった、今後のストーリー展開に期待
        - 書籍というプロジェクトの性質のソフトウェアとの違いがどう影響するか気になるところ

まとめ<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
- ![image](https://gyazo.com/ae1acdb372c8ed350fb9d8d539433d4d/thumb/1000)
- 前回の勉強会では、Plural Managementの概要を把握することができました。Plural Managementは、階層的な組織構造とフラットな分散型組織の望ましい特性を組み合わせたプロトコルであり、個人の貢献と管理決定に基づいて管理権限を動的に割り当てることを目指しています。
- 今回の勉強会では、Plural Managementの中核をなすQuadratic VotingとQuadratic Fundingについて深く掘り下げました。Quadratic Votingは、参加者が投票によって「意見の強さ」を表現できるように設計された投票システムです。従来の一人一票制では、個人の選好の強さを反映することができませんでしたが、Quadratic Votingでは、強い主張ほど高いコストがかかるようにすることで、選好の強度を投票に反映させることが可能になります。
- Quadratic Votingの数学的根拠についても理解を深めました。投票のコスト関数を二次関数にすることで、投票結果と「気持ちの強さ」の合計が一致するようになります。これにより、集団的意思決定における公平性と効率性が向上すると期待されます。
- Quadratic Fundingは、Quadratic Votingのアイデアを公共財への資金提供に応用したものです。GitcoinのようなプラットフォームでQuadratic Fundingが実践されており、コミュニティにとって価値の高いプロジェクトへの投資が促進されています。
- 前回のPlural Managementの議論と今回のQuadratic VotingとQuadratic Fundingの理解を合わせることで、Plural Managementの仕組みがより明確になりました。組織のメンバーがマネジメント・クレジットを獲得し、それを使って課題の優先順位付けや貢献の評価に参加することで、ダイナミックで実力主義的な権力構造が形成されます。
- Plural Managementはまだ発展途上の概念ですが、従来の組織構造の問題点を解決し、より適応的で集合知を活用する組織運営を可能にする可能性を秘めています。今後、実際の組織でPlural Managementを導入する際の課題や、システムの調整方法などについてさらなる研究が必要だと感じました。
- 手直ししなくてもこのままでまとめとしてOKだと思った<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

質疑
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. 例えば「200-年齢」を投票権として持つようにしたらいい気がしてきた
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. それは「高齢者の発言力が高すぎるので減らしたい」という日本の若者の視点からは改善の一つのアプローチですが、年齢という属性によって票数が影響されるシステムは「損をする属性の人と得をする属性の人」の分断を招くという考え方があります。Quadratic Votingは属性による分断を招かずに、自分の興味によってウェイトを変えられるのが強みです。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. 死に票が減る減らないみたいな話とQVは独立した話なんでしょうか？
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. Quadratic Fundingでは、どの1票も「いくら分配されるか」に寄与するので、「意思決定に反映されない死に票」は存在しません。Quadratic Votingでは、投票しても結果が変わらないシチュエーションは発生しますが、そう思うなら投票しないで票を持ち越すことができるので「投票したけど価値がゼロ」ということは起こりません。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. 投票者が普通の投票よりQVのほうがいいな！って感じるのってどういうとき？
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. 意見の強さを表明できること、複数の選択肢に投票できることがメリットとして挙げられます。投票対象に興味がないときに票を持ち越せることもメリット、ただしこれはトークンに継続価値がある場合の話。台湾総統杯ハッカソンの99票の仕組みは、むしろQuadratic Votingの良さというよりは、面白いUIの工夫だと思います。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. QVは整数でしか投票させないのか
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. そういう制約はQV自体にはないです。台湾総統杯ハッカソンではそれをやっているだけです。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q. 複数投票するインセンティブを別途与えたらよいのでは(コストを追加配分してあげるなど)
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>A. そういうUXの設計を色々試行錯誤していくのもいいかもですね

- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>Q: ある人の投票の効用を潰すために、その人が高いコストを投票しそうな議題を分割してたくさんに増やす、という戦略が取れる？
    - A: 議題をコントロールできる人がいて、その人が特定の人に不利なような議題を立てることができるなら、そういう攻撃は成立しうる。この場合は「議題をコントロールできる権力」の悪用が問題なのでAudrey Tangは「[[アジェンダ設定の権限を人々に開放する]]」べきだと主張している。

- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>[[トークンエコノミー]]のめっちゃいい事例ですね

「投票クーポン」の議論
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>この会話では、投票に参加するインセンティブとして「投票クーポン」のアイデアについて話しています。このクーポンは、投票に参加することで得られ、次の投票機会で使用できるというものです。さらに、複数投票がある場合には、その場でクーポンが増える可能性があるという提案も出ています。また、自分の支持した選択肢が採用されなかった場合には、クーポンが返されることで、すべての参加者がある程度の満足感を得られるような仕組みについても議論されています。
    - 投票クーポンの提案: 投票に参加するとクーポンがもらえ、次回の投票機会で使用可能。これは投票への参加を促すインセンティブとなる。
    - クーポンの増加: 複数投票の場合、投票時にクーポンが即座に増える可能性がある。これは、よりアクティブな参加を奨励するメカニズムとして機能する。
    - クーポンの返却: 支持した選択肢が採用されなかった場合にクーポンが返される。このアイデアは、死に票（得票が少なく結果に影響しない票）を減らす方法として、またすべての参加者に一定の満足感を提供する方法として提案されている。
- このシステムの目的は、参加者により公平な感覚を提供し、投票への参加意欲を高めることにあります。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>QVの観点からコメントして
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Quadratic Voting（QV）の観点から、提案されているアイデアについて考察します。
    - 投票クーポンの導入： 投票に参加することで投票クーポンをもらえるシステムは、参加促進のメカニズムとして興味深いです。QVの文脈では、これらのクーポンは将来の投票で使用できる「声の強さ」を表すことになります。つまり、より多く参加することで、将来的に自分の意見を強く主張できる権利が増えるわけです。このアプローチは、参加者に対して長期的な参加を促し、投票システムへの関与を深める可能性があります。
    - 次の投票機会に使えるクーポン： クーポンが次の投票機会にのみ使えるという制約は、参加者が定期的に投票プロセスに関与し続けるインセンティブを提供します。これにより、継続的な参加が促され、コミュニティの意思決定プロセスにおける活動的な参加者の基盤が強化されるかもしれません。
    - 複数投票によるクーポンの増加： QVの枠組みの中で、複数の選択肢に投票することでクーポンが増えるというのは、投票者に多様な意見を考慮し、より広範な議題に投票するインセンティブを与えます。これにより、一つの議題や候補者に対する過度の票の集中を避け、よりバランスの取れた意思決定を促す効果が期待できます。
    - 希望が通らなかった場合のクーポン返却： QVでは、投票のコストは選択肢に投じた票数の二乗に比例しますが、希望が通らなかった場合に投票クーポンを返すシステムは、死に票を減らし、参加者にリスクを取っても良いという安心感を与えます。これは参加者が自分の意見を積極的に表明することを奨励し、より公正で包括的な意思決定プロセスに貢献する可能性があります。

未使用断片
- コーポレート・ガバナンス(2014): Posner, E. A., & Weyl, E. G. (2014). Quadratic voting as efficient corporate governance. The University of Chicago Law Review, 81(1), 251-272. [PDF](https://chicagounbound.uchicago.edu/cgi/viewcontent.cgi?article=1642&context=law_and_economics)
    - 株主の議決権決定に使う案

