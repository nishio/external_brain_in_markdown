---
title: "Plural Management勉強会"
---

2024-01-26 [[サイボウズラボ勉強会]]
- [[尾鷲2024-01-23~24]]行ってて準備時間が無かったのでショートバージョン
- 今回の目的: 1/9に公開されたばかりの[[Plural Management]]を読む
- 追記: この次の回に改めて[[Quadratic VotingとPlural Management勉強会]]をやった

# Plural Management
- > We introduce Plural Management, a model for partially replacing hierarchical organizational authority with plural mechanisms allowing networked authority. Participants earn influence by anticipating and fulfilling organizational priorities and harness this influence to set priorities and validate contributions, fostering a dynamic, merit-based power structure. This approach, which we illustrate with the example of open-source software development, emphasizes valued contributions and diligence without requiring hierarchical choke points, thereby enhancing participation and allowing adaptive collective intelligence.
- > Keywords: management, plurality, [[quadratic mechanism]]s, open-source, software management, organizational dynamics
- > [[階層的な組織の権威]]を、[[ネットワーク化された権威]]を可能にする[[Pluralなメカニズム]]に部分的に置き換えるモデルである「[[Plural Management]]」を紹介する。参加者は、組織の優先順位を予測し、それを達成することによって影響力を獲得し、この影響力を利用して優先順位を設定し、貢献を検証することで、ダイナミックで[[実力ベースの権力構造]]を育成する。[[オープンソースソフトウェア開発]]を例に説明するこのアプローチは、階層的な隘路を必要とすることなく、[[価値ある貢献]]と[[勤勉さ]]を強調し、それによって[[参加]]を強化し、[[適応的な集合知]]を可能にする。
- > キーワード：マネジメント、[[Plurality]]、[[二次的メカニズム]]、[[オープンソース]]、[[ソフトウェアマネジメント]]、[[組織力学]]
- [paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4688040)
    - Date Written: January 9, 2024
        - できたてホヤホヤ！
- 著者の一人が[[Glen Weyl]]
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>力がある人が権力を握る世界？
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>それはトートロジーでは？
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>実力主義で考えると、実力がある人にこそ権力を持ってほしい。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ああ、なるほど実力ベースの権力構造の部分の話か。
        - [メリトクラシー - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%A1%E3%83%AA%E3%83%88%E3%82%AF%E3%83%A9%E3%82%B7%E3%83%BC)
            - > 個人の持っている能力によってその地位が決まり、能力の高い者が統治する社会を指す。
        - この言葉は後で出てくる

先に釘を刺しておく
- 世の中に時々民主的システムに関する不毛な論戦がある
- その原因の一つは下記の2タイプの人が喧嘩をすること
    - A: 「民主的であることは善である」と思考停止してるアホ
    - B: 会話の中に民主的という言葉が出てきただけで「Aのタイプのアホ」と決めつけるアホ
- その「民主的システム」が具体的にどういう目的で何をどうするシステムなのかをきちんと掘り下げて考えなければいけない
    - 基本的にどんなシステムも「万能の魔法」「銀の弾丸」ではなく、適材適所で使わなければならない
    - 「今の民主的システム」も色々なシチュエーションで機能不良が起きている
    - 「新しい民主的システム」が問題解決のために提案される
    - そのシステムを知らなければ適切な対象に対して「これに使おう」と思いつくことはできない

# [[Gov4git]]
- 抽象的な話をする前にイメージをわきやすくするために実際に動くソフトウェアをみよう
- Plurality Bookの執筆プロジェクトで使われている[[Gov4git]]
- Plurality Bookに長く貢献しているakinoriさんの画面
    - ![image](https://gyazo.com/df5184460b4dce6d06c04d9bfa407fe6/thumb/1000)
    - [/plurality-japanese/Social Hack Day雑談後半#65ab7832aff09e0000b14451](https://scrapbox.io/plurality-japanese/Social Hack Day雑談後半#65ab7832aff09e0000b14451)
- GithubのIssuesに対して[[Quadratic Voting]]での投票ができる
    - Vote creditsは貢献によって得られる
    - 上記スクリーンショットでは11票を投じようとしている、そのためには11の二乗の121クレジットを支払う必要がある
- 僕のGov4gitの画面でGithubとのインテグレーションについてのデモをする
- ![image](https://gyazo.com/7b8f2e8440ab6ac09c81033453ca32b7/thumb/1000)
    - GithubのIssues
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>オープンソースで使われているgitの仕組みを応用しているってことなのかな。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>というか[これ](https://github.com/pluralitybook/plurality/labels/gov4git%3Amanaged)普通にGithubのissues。Github上で管理されてるOSSプロジェクトで使われている。
        - `gov4git:managed`というラベルのついたイシューがgov4gitで管理される
- ![image](https://gyazo.com/9ee28bae96a0469437d8202c8f0b5493/thumb/1000)
        - gov4gitアプリではこんな感じで管理対象のissuesが見える
    - ![image](https://gyazo.com/1094e4a8faf14b0aecc88ca2bc4e0f62/thumb/1000)
        - ここで投票できる
    - ![image](https://gyazo.com/40264eb81228b6a822c18fd8d7b68427/thumb/1000)
        - イシューに対してグレンがラベルをつけてる、botがそれを読んで管理対象にする
    - ![image](https://gyazo.com/945e35ef5c481505b661d8b93578d9d2/thumb/1000)
        - 誰かが投票すると優先度の値が変わる
- 参考資料: [Gov4Git community dashboard · Issue #263 · pluralitybook/plurality](https://github.com/pluralitybook/plurality/issues/263)
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>なんで二乗にしたんだろう。いろいろチューニングできそうな項目だなあ。
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>この「二乗」の考えかたは興味深い（納税額の平方根で追加の投票ができたらどうなるのかな？）。
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>それが[[Quadratic Voting]]
    - [[Quadratic Voting: How Mechanism Design Can Radicalize Democracy]]
        - Steven Lalley, E. Glen Weyl (2018)
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>数学的な根拠があるのか！！
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 自分一人が100倍稼ぐのと、同じ意見を持った人を10人集めるのが同じ価値。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> Yes


Plural Management
- ![image](https://gyazo.com/f1adcb67a3ac4116d16d0425c7ebd729/thumb/1000)
- > 組織のメンバーは、仕事を通じてマネジメント・クレジットを動的に獲得することができる。イシュー・ボードでは、クレジットを使った二次関数的な資金調達([[Quadratic Funding]])によって、メンバーが課題に優先順位をつけることができる。これらのクレジットは、貢献によってこれらの課題に取り組むメンバーに支払われる。支払いは、権限を行使するためにマネジメント・クレジットを消費する他のメンバーによって行われる二次投票の後にのみ行われる。
- >  組織の管理者は、投票結果を正しく予測したり、貢献に対するデューデリジェンスで個人に報酬を与えたり、既存の管理者の好みを予測したりすることで、メンバーが管理クレジットを獲得できるようにすることを選択できる。
- >  このプロトコルは、単純化された階層を持たない小さなメンバーの集まりから大きな組織までスケールするメカニズムを通じて、ダイナミックな管理制御を可能にする。

# 1 Introduction
- > The standard dichotomy between the rigidity of hierarchi- cal organizations and the fluidity of flat configurations is a basic challenge for organization design. Traditional hier- archies with clear command structures are still the norm but are often seen as stifling the dynamic capabilities or- ganizations need to thrive in today’s complex landscape. Conversely, flat structures, while inclusive and dynamic, often struggle to maintain coherent direction, momentum, and accountability, often falling into the “[[tyranny of structurelessness]]” ([[Ostrom and Hess, 2011]]).
- > 伝統的な階層型組織の硬直性と、フラット型組織の流動性との間の標準的な二分法は、組織設計における基本的な課題です。明確な指揮構造を持つ伝統的な階層制は依然として一般的ですが、今日の複雑な環境で組織が繁栄するために必要なダイナミックな能力を抑制していると見なされることが多いです。逆に、包括的でダイナミックなフラット構造は、しばしば一貫した方向性、運動量、責任感を維持することに苦労し、「構造のない専制」に陥ることが多い（オストロムとヘス、2011）。
    - [The Tyranny of Structurelessness - Wikipedia](https://en.wikipedia.org/wiki/The_Tyranny_of_Structurelessness)
    - 階層的マネジメントは硬直的だ〜という批判があるが、じゃあ階層がない組織構造にしたらうまくいくかというと、誰もリーダーシップを発揮しなくてぼんやりとお互いの様子を見てるだけになったりする、ありがちだよね
    - [[社会的手抜き]]
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> なるほど、フラットすぎるとリーダー不在で非効率になる、と。
- > The classic alternative to this dichotomy is the use of markets (Hamel and Zanini, 2020; Coase, 1995). Yet, a critical role of firms is to create internal partially public goods and take advantage of increasing returns, which markets generally do not efficiently supply (Samuelson, 1995). Thus Groves (1973) and Groves and Loeb (1979) argued for using public goods mechanisms to organize pro- duction inside firms in lieu of hierarchies and markets. Yet, these mechanisms have typically been seen as cum- bersome and impractical.
- > この二分法への古典的な代替案は市場の利用です（ハメルとザニーニ、2020年；コース、1995年）。しかし、企業の重要な役割は、部分的に公共の財を内部で創出し、市場が通常効率的に供給しない増加収益を利用することです（サミュエルソン、1995年）。したがって、グローブス（1973年）とグローブスとローブ（1979年）は、階層や市場に代わって企業内の生産を組織するために[[公共財メカニズム]]を使用することを主張しました。しかし、これらのメカニズムは通常、煩雑で実用的ではないと見なされてきました。
    - 市場は分業すれば効率的になるようなタスクに関しては効率的に協働を引き起こす
        - 僕がパンを食べる時に「小麦を育てる人」「粉を作る人」「パンを焼く人」が協力している
    - 一方で、なぜ企業があるかというと、ある種のタスクに関しては社外から調達するよりも、人間を雇用して社内で生み出した方が効率的だからだ
    - なぜ効率的なのかというと、社外にはない「効率的に生み出す仕組み」が社内にあるからだ
        - [初公開！　サイボウズの自由すぎる働き方はこんなやり方で管理されていた | サイボウズ式](https://cybozushiki.cybozu.co.jp/articles/m005338.html)
- > Recently, however, variants on these public good mech- anisms, especially Quadratic Voting (Lalley et al., 2016) and Quadratic Funding (Buterin et al., 2019), have been increasingly broadly and successfully applied1. This pa- per seeks to harness these advances to return to Groves’s agenda and outline a framework we call “Plural Manage- ment” that combines these with other successful mechanisms to mimic many features of organizational authority and collaboration without requiring simplistic hierarchy.
- > しかし最近では、これらの公共財メカニズムの変種、特に[[Quadratic Voting]]（ラリー他、2016年）や[[Quadratic Funding]]（ブテリン他、2019年）が、広範囲にかつ成功裏に適用されています。本論文は、これらの進歩を活用してグローブスのアジェンダに戻り、「[[Plural Management]]」と呼ばれる枠組みを概説し、これらを他の成功したメカニズムと組み合わせて、単純な階層を必要とせずに組織の権威と協力の多くの特徴を模倣します。
    - この数年の間に、QV、QFがあちこちで使われるようになっていて、これを公共財のマネジメントに使ったらいいんじゃないか？という話になったので今回の論文ができた
- > Traditional hierarchical management systems, the backbone of modern corporate and organizational struc- ture, are predicated on power dynamics that traditionally follow a top-down approach (Drucker, 1974). Employees within such systems often climb the ladder by demon- strating value through hard work and alignment of their actions with a culture articulated by those in authority, a practice sometimes pejoratively caricatured as ‘sucking up.’ Detractors note that such practices can suppress cre- ativity, reduce employee engagement, create bottlenecks in decision-making, and often result in the underutiliza- tion of talent at lower levels of the organization.
- > 伝統的な階層型管理システムは、現代の企業や組織構造の基盤であり、伝統的には上から下へのアプローチに従う力のダイナミクスに基づいています（Drucker、1974年）。そのようなシステム内の従業員は、一般に、権力者によって表現された文化に自分の行動を整合させ、労働を通じて価値を示すことによって階層を登ります。これは時に、「おべっか使い」として揶揄されることもあります。批評家は、そのような実践が創造性を抑え、従業員のエンゲージメントを低下させ、[[意思決定におけるボトルネック]]を生み出し、組織の下層での[[才能の未活用]]にしばしばつながることを指摘しています。
    - [[top-down approach]] / [[上意下達]]
    - 上司の意見に逆らうとネガティブな評価を受けると感じることによって、上司が要求しているものを満たすことだけに注力し、衝突が起きる可能性のある「新しいもの」を部下が出さなくなる
        - これが「[[才能の未活用]]」
        - それによって上司の能力で組織の能力が決まる[[ボトルネック]]が発生する
- > At the other end of the spectrum, the absence of struc- tured management has its pitfalls, such as the ‘tyranny of structurelessness,’ where the lack of clear roles and re- sponsibilities can lead to chaos, inefficiency, and the emer- gence of informal and often unaccountable power struc- tures (Friedman, 2007). Striking a balance between overly rigid hierarchies and a complete lack of structure has been a complex endeavor. Several innovative manage- ment approaches have been proposed and widely imple- mented, such as flat organizations that minimize hierar- chical levels (Laloux, 2014), holacracy which distributes decision-making through overlapping teams (Robertson, 2015), and sociocracy which emphasizes consensus in gov- ernance (Buck and Endenburg, 2012). Each of these mod- els seeks to address the limitations of traditional hierarchy by promoting a more egalitarian and adaptive approach (Rothschild and Whitt, 1986). None, however, has the mechanistic clarity of either markets or hierarchies, ar- guably undermining their capacity to avoid the challenges Freeman highlights. We aim to harness advances in plural mechanism design to fill this lacuna.
- > 一方で、構造化された管理の欠如にも問題点があります。例えば、「構造のない専制」という状況があり、ここでは明確な役割と責任の欠如が混乱、非効率、そしてしばしば無責任な非公式な権力構造の出現につながります（フリードマン、2007年）。過度に厳格な階層と全くの構造不足の間のバランスを取ることは複雑な挑戦です。いくつかの革新的な管理アプローチが提案され、広く実施されています。たとえば、階層レベルを最小限に抑えるフラット組織（ラルー、2014年）、意思決定を重複するチームを通じて分配するホラクラシー（ロバートソン、2015年）、統治におけるコンセンサスを強調するソシオクラシー（バックとエンデンブルグ、2012年）などです。これらのモデルは、より平等で適応性のあるアプローチを推進することで、伝統的な階層の限界に対処しようとしています（ロスチャイルドとウィット、1986年）。しかし、これらの方法はいずれも、市場や階層のような明確なメカニズムを持っておらず、フリーマンが強調する課題を回避する能力に疑問があると言えます。私たちは、複数メカニズム設計の進歩を活用して、この空白を埋めることを目指しています。
    - [[ティール組織]]の中でも色々語られてきた
    - サイボウズも実践的に模索している領域
        - [サイボウズの開発本部がマネジャーをなくしてみた「いないと無理なら、またつくればいい」 | サイボウズ式](https://cybozushiki.cybozu.co.jp/articles/m005343.html)
    - これらの色々なアプローチに「うまく行かせるためのメカニズム」が明確に定義されてない
        - コミュニティマネジメント能力の高い個人の力量でうまく回ってるだけかも？
        - [[メカニズムデザイン]]によって、うまく行かせる構造を作れないか？というのがこの研究のアプローチ
- > In the proposed model, management credits serve as a dynamic ledger of contribution and influence. Internal, non-financial credits are initially assigned based on role or past contributions and are subsequently earned through direct contributions and triage. The expenditure of these credits in setting priorities and approving contributions is governed by a quadratic cost function, steering towards optimal public goods outcomes by avoiding excessive dom- inance of those with greater authority. Prediction markets are used to encourage those with limited authority to act as “analysts”, helping authorities triage contributions, and dynamic evolution of priorities on unaddressed tasks act as a sort of dynamic auction-like bounty system to en- sure tasks are addressed in a timely and well-prioritized manner.
- > 提案されたモデルでは、管理クレジットは貢献と影響力の動的な台帳として機能します。内部の非財務的クレジットは、役割や過去の貢献に基づいて最初に割り当てられ、その後、直接の貢献や優先順位付けを通じて獲得されます。これらのクレジットの使途は[[二次関数的なコスト関数]]によって管理され、より権限のある者の過度な支配を避けることで、最適な公共財の結果に向けて誘導します。[[予測市場]]は、権限の限られた者が「アナリスト」として機能し、権威者が貢献を選別するのを助けるために使用され、未解決のタスクに対する優先順位の動的進化は、タスクがタイムリーかつ優先順位が高い方法で対処されることを確実にするための動的な[[オークション]]のような報奨金システムのようなものとして機能します。
    - [[二次関数的なコスト関数]]
    - [[予測市場]]
    - [[オークション]]
    - などなどの要素を組み合わせている
- > We thus aim to combine the flexibility and dynamism of flat structures, the clear and transparent incentives of markets, and the collective orientation and strategic di- rection provided by traditional management. While for concreteness we focus on a fully specified design that will be deployed in several near-term applications that we dis- cuss, we fully expect significant further improvement on these mechanisms as we discuss in the conclusion and thus aim to suggest as much a general structure for combining mechanisms to achieve this synthesis as the specific design we use to illustrate this structure.
- > したがって、私たちはフラット構造の柔軟性とダイナミズム、市場の明確で透明なインセンティブ、そして伝統的な管理によって提供される集団的な方向性と戦略的な指向を組み合わせることを目指しています。具体性のために、我々が議論するいくつかの近い用途で展開される完全に特定されたデザインに焦点を当てますが、結論で議論するように、これらのメカニズムにさらなる大幅な改善が期待されるので、この合成を達成するためのメカニズムの組み合わせのための一般的な構造としてだけでなく、この構造を説明するために使用する具体的なデザインを提案することを目指しています。
    - 固定的な階層を導入しないことによる柔軟さと、ガバナンスクレジットの導入による透明性と、伝統的な「組織が一丸となって進むべき方向性を決めること」のいいとこどりをしたいという話
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>企業内で使うときは、OSSへの貢献ポイントに変わる通貨として何を使うといいんだろう
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>後で出てくる
- > The rest of this paper is organized as follows: Sec- tion 2 presents the [[Plural Management Protocol]], detail- ing the high-level description of the system, roles within the ecosystem, and the processes of earning and spending management credits. It goes on to discuss the practical ap- plication of the Plural Management system in the context of open-source software development, illustrating how it can help address long-standing problems of management in open-source projects as they scale. Section 3 elabo- rates on this to provide a more detailed technical version of the protocol suitable for implementation. In Section 4, we provide a detailed analysis of the protocol properties, examining the voting and prediction behaviors and the optimal parameter choices within the system. Lastly, Sec- tion 5 examines some implications of such a protocol and highlights the open questions and future work it presents.
- > 本論文の残りの部分は次のように構成されています：セクション2では、プルーラル・マネジメント・プロトコルを紹介し、システムの概要、エコシステム内の役割、および管理クレジットの獲得と消費のプロセスについて詳述します。さらに、オープンソースソフトウェア開発の文脈でプルーラル・マネジメント・システムの実用的な応用について議論し、スケールアップする際のオープンソースプロジェクトの長年の管理上の問題にどのように対処するかを示します。セクション3では、実装に適したより詳細な技術的バージョンのプロトコルについて詳述します。セクション4では、プロトコルの特性の詳細な分析を行い、システム内の投票と予測行動、および最適なパラメーター選択について検討します。最後に、セクション5では、そのようなプロトコルのいくつかの意味合いを検討し、それが提示する未解決の問題と今後の作業についてのハイライトを行います。
    - 時間もないし今回は4を飛ばすのが良いと思う

# 2 Plural Management Protocol
- ![image](https://gyazo.com/86d0c416d328bda9e40d30ec804828d8/thumb/1000)
- > There are three roles in the ecosystem: workers, who make direct contributions to an organization; managers, who determine what work is important and whether a piece of work is of acceptable quality; and administrators, who can determine system properties to sway behavior. Im- portantly, an individual can act in multiple of these roles at any given time and in relation to multiple other indi- viduals; no role is fixed and members of an organization are encouraged to act in a diversity of roles with respect to a diversity of other individuals.
- > エコシステム内には、組織への直接の貢献を行う「労働者」、どの作業が重要であり、作業の品質が受け入れられるかを決定する「マネージャー」、そして行動を誘導するためにシステムの特性を決定できる「アドミン」の3つの役割があります。重要なことは、個々の人が、任意の時点でこれらの役割の複数を果たし、複数の他の個人と関連して行動することができるということです。役割は固定されておらず、組織のメンバーは多様な他の個人に対して多様な役割で行動することが奨励されます。
    - 役割が固定していない
    - ![image](https://gyazo.com/505549b07145e90fc3ae6e94b8e9f078/thumb/1000)
- > Instead of a set of hierarchical roles assigned to an in- dividual, each person has a set of management credits for this organization. These credits allow an individual to ex- ercise authority in decision-making and be recognized for contributions made. We walk through each step where credits are gained and spent. These credits are specific only to a particular organization, project, or community and have no value outside of it; in this sense they are similar to a “community” or “artificial” currency (Blanc, 2018). As we discuss later, these credits cannot be traded externally; they serve only to control the flow of dynamic management potential.
- > 個人に階層的な役割のセットを割り当てるのではなく、各人はこの組織のための管理クレジットのセットを持っています。これらのクレジットにより、個人は意思決定において権威を行使し、貢献が認識されることが可能になります。我々は、クレジットが得られ、使われる各ステップを詳しく説明します。これらのクレジットは特定の組織、プロジェクト、またはコミュニティにのみ固有のものであり、外部では価値がありません。この意味で、それらは「コミュニティ」や「人工的な」通貨に似ています（ブラン、2018年）。後述するように、これらのクレジットは外部で取引されることはなく、動的な管理ポテンシャルの流れを制御するためにのみ使用されます。
    - 組織の外で流通することを目指したトークンではないし、だから給与の一部を仮想通貨で払うとか、同僚から感謝トークンを集めたらボーナスが増えるとかそういう金銭的インセンティブに基づくものではないよ、ということ
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これが<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>企業内で使うときは、OSSへの貢献ポイントに変わる通貨として何を使うといいんだろうの回答
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>同僚から感謝トークンを集める？
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>いいね数を稼ぐのと同じ感じ？
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>「感謝トークン」が「いいね」みたいにゼロコストで無限に湧いてくるものをイメージしているなら、それとは違う。限られた量のトークンしか持ってない
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 貨幣とトークンの取引を防ぐ仕組みの維持は結構大変そう……
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 後で出てくるけど、個人間のトークンの譲渡はできない
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> そこで、架空のタスクをつくってですね……
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 取引相手以外の人がプルリクをする可能性があるし、仮に取引相手がプルリクしても(3)の貢献投票の段階でリジェクトされそう
            - ![image](https://gyazo.com/34dbf5a296e61126d6d892bce2b3e766/thumb/1000)
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> QVにより大きく減額されちゃう
                - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>どうだろ、もらえるトークンは平方根を取る前のものだと思う。さもないとすごい勢いでトークンが減っていってしまう
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> RMTの穴を全部埋めるのは無理でしょうね
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 実際にポイントを渡せなくても、私の代わりにお前も〇〇に寄付しろ、は言えそう。
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 談合([[collusion]])の問題ね、後で出てくるけど [[Beyond Collusion Resistance: Leveraging Social Information for Plural Funding and Voting]] などの研究がある
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>タスクを処理したら、タスクに投票されていたクレジットをもらえる、という仕組みだと、最初の原資がどこから来るのか。
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 時間経過で湧いてくるとか、プロジェクト開始した人が持ってて後から来た人に分配するとか
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> issueが解決されたという判断はissueの依頼者がするのかな
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> (3)のVotingで行われる
- > Consider an organization that has an issue board where all major tasks or initiatives to be completed are listed (similar to open-source issue trackers as in subsection 2.1). Individuals with management credits can set priorities for an organization by assigning a priority value for an is- sue using credits. The priority on an issue is not simply the sum of the credits assigned to it, but instead may be matched by a matching pool (provided by individuals in their role as administrators) consistent with practical ap- plications of Quadratic Funding, as we will discuss further below.
- > すべての主要なタスクやイニシアティブがリストされた問題ボードを持つ組織を考えてみましょう（サブセクション2.1のオープンソースの問題トラッカーに似ています）。管理クレジットを持つ個人は、クレジットを使用して問題に優先順位を割り当てることで、組織の優先順位を設定できます。問題に割り当てられたクレジットの合計ではなく、実際の二次資金調達の応用に一致して、管理者としての役割を果たす個人によって提供されるによるマッチングプールによってマッチングされる場合があります。
    - 雑に言えばたくさんクレジットを持っている個人が他の人の参加のインセンティブを増やすために寄付することができるよ、という感じ
        - ここまでの話で企業内のユースケースを話していたから「参加のインセンティブ？」となりそう
        - 例えば社内の非エンジニア部門が抱えているちょこっとJSを書けば解決したりするような問題をエンジニアたちが解決するハッカソンをしましょう的なシチュエーションを考えると「そういう活動が行われるのはいいことだね」と思った個人が自分のトークンをマッチングプールに入れることができる
        - そうすると実際にコードを書いて問題を解決するエンジニアに対するとーくんのしはらトークンの支払いが増えるので、より参加を促すインセンティブになる
        - エンジニアがより一層参加するなら、自分の課題をイシューボードに登録しておこうというインセンティブが課題オーナー側でも高まる
        - 結果として「こういう活動が行われるのはいいね」というトークン寄付が活動自体への他のメンバーの参加を促す

- > An individual may perform the role of a worker and provide a solution to an issue in the form of a contri- bution. If this contribution is accepted, the worker will receive credits proportional to the total number of cred- its assigned in the priority setting. In essence, from a worker’s perspective, the ‘bounty’ attached to an issue may go up over time similar to a reverse Dutch auction, until a sufficient reward is offered to compensate the cost to the worker of addressing the issue, though there is not a necessary guarantee that the reward will increase over time.
- > 個人は労働者の役割を果たし、貢献という形で問題の解決策を提供することができます。この貢献が受け入れられた場合、労働者は、優先順位設定で割り当てられたクレジットの総数に比例するクレジットを受け取ります。本質的には、労働者の視点からは、問題に付随する「報酬」が、労働者が問題に取り組むコストを補償するのに十分な報酬が提供されるまで、逆オランダ式オークションのように時間とともに上昇する可能性がありますが、報酬が時間とともに増加する保証は必ずしもありません。
    - 数学的な保証はないが、雰囲気としては「誰も解決してくれなかったけど、これは解決が必要」というイシューはだんだん追加のクレジットを集めて、それをやった時に労働者が得るクレジットが増える感じがある
- >  Once a contribution has been made, it goes to a con- tribution vote. In this vote individuals can expend man- agement credits to vote if the contribution should be ap- proved or not. If the vote passes, the worker is rewarded; if not, the issue returns to the board (wherein managers can increase the priority to provide a higher bounty). This vote is done quadratically, this ensures a balanced impact between individuals with varying credit amounts.
- > 貢献が行われると、貢献投票に進みます。この投票で個人は管理クレジットを消費して、貢献が承認されるべきかどうかを投票できます。投票が通過すると、労働者に報酬が与えられます。そうでない場合は、問題がボードに戻ります（管理者は優先順位を上げてより高い報酬を提供できます）。この投票は二次的に行われ、これにより、さまざまなクレジット量を持つ個人の間でバランスの取れた影響が保証されます。
    - 貢献が行われた後には、それが貢献として適切であるかどうかのレビューが必要
        - Git上でのOSSでイメージするとわかりやすい
        - いきなりコミットを許すのではなく、プルリクエストを見てマージするかどうかの判断が必要
        - それを投票で行って良いの？という気持ちになると思うが、先で色々説明するのでここは先に進む
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>これが<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> issueが解決されたという判断はissueの依頼者がするのかなの回答
- > In addition to casting a vote, each individual can choose to ‘bet’ the number of credits they used to vote that their prediction of acceptance or rejection will suc- ceed. If correct, this bet will pay out double the credits used to vote. This vote prediction allows individuals to be rewarded for correctly anticipating the desires of the full community. We introduce a prediction subsidy parameter that can be set by administrators for each contribution vote that reduces the cost of voting and increases the re- ward from betting. By default, voting and then betting on this is strictly unprofitable. However, in many cases, ad- ministrators may wish to increase the subsidy to allow op- portunities for individuals who can anticipate community needs to gain authority. For example, providing a subsidy can incent individuals with fewer management credits to participate in votes that would otherwise be costly, which means that a larger crowd of individuals is performing due diligence on contributions. If many contributions are being made in a large organization, this is akin to reward- ing individuals for administrative processing that “triages” contributions and thus surfaces important divisive votes to managers with more authority.
- > このモデルでは、個々の人は投票に加えて、自分の受け入れまたは拒否の予測が成功するかどうかに投票に使用したクレジット数を「賭ける」ことを選択できます。予測が正しい場合、この賭けは投票に使用したクレジットの2倍の支払いをもたらします。この投票予測により、個人はコミュニティ全体の願望を正確に予測することに対して報酬を受け取ることができます。私たちは、投票のコストを削減し、賭けからの報酬を増加させるために、管理者によって各寄稿投票に設定される予測補助パラメータを導入します。デフォルトでは、投票して賭けることは厳密には非収益性です。しかし、多くの場合、管理者はコミュニティのニーズを予測できる個人に権限を与える機会を提供するために補助金を増やすことを望むかもしれません。例えば、補助金を提供することで、管理クレジットが少ない個人が、それ以外ではコストがかかる投票に参加することを奨励できます。これは、より多くの人々が貢献への適切な注意を払っていることを意味し、大きな組織内で多くの貢献が行われている場合、これは「貢献の選別」を行い、より多くの権限を持つ管理者に重要な分岐点の投票を浮き彫りにするための管理処理に対する個人の報酬と見なすことができます。
    - つまり予測市場の仕組みによって、例えば「一人のコミッターXが受け入れるかどうかを意思決定しているプロジェクト」がこのシステムに移行した場合、他の人たちが「Xの判断が信頼できる」と思っているならXの評価と同じ投票をするので結果的に同じことになる
    - 個人的には「Xが投票するまで自分の投票を遅らせよう」というインセンティブが発生してしまうのではという気がする
        - Xが一人で判断していた時には、Xに常に判断の重荷が全部集中していた
        - Xが常に評価をする保証がなくなると、強い意見のある人は先に評価投票をするようになる？
            - 誰も投票しないなら自分が安い投票をするだけで自分によって都合のいい結論になるから
- >  Put together, these two systems of quadratic agenda setting and hybrid voting-prediction can create a dynamic system of management, where contributions are rewarded in proportion to their public good demand when the broader organization collectively approves of them and individuals who have developed a robust understanding or model of the community preferences are rewarded and empowered for supporting administrative processes.
- >  二次的な議題設定と投票・予測のハイブリッドシステムの組み合わせは、公共財の需要に応じて寄稿が報酬を受け、より広範な組織がそれらを集団的に承認した場合、およびコミュニティの好みの堅牢な理解やモデルを開発した個人が管理プロセスをサポートすることで報酬を受け、権限を与えられる、動的な管理システムを作り出すことができます。
    - まあ動的になるのは間違いないだろうな
    - よくなるかどうかは不明

# 2.1 An application to open-source
- ここからオープンソースプロジェクトの話
- >  Although the plural management protocol can be applied across a wide range of organizations and communities, it has particular relevance to the world of open-source soft- ware and other spaces where peer production is common (Benkler, 2017). Far from being a niche industry, git- based open-source powers over 93% of all modern soft- ware applications (Daigle, 2023), and already operates via community models of governance, where contributions in the form of code are assessed for quality and relevance before being merged into existing work. Despite these im- portant contributions, open-source communities are well- known for their governance and management challenges, documented most famously by Eghbal (2020) and includ- ing the following:
- > プルーラル・マネジメント・プロトコルは幅広い組織やコミュニティに適用できますが、特にオープンソースソフトウェアやピアプロダクションが一般的な分野での関連性があります（ベンクラー、2017年）。オープンソースはニッチな産業から遠く、gitベースのオープンソースは現代のソフトウェアアプリケーションの93％以上を支えています（ダイグル、2023年）。また、コミュニティのガバナンスモデルを介して運営されており、コードの形での寄稿が品質と関連性に基づいて評価され、既存の作業に統合されることがあります。これらの重要な貢献にもかかわらず、オープンソースコミュニティは、エガル（2020年）によって最も有名に文書化されたように、ガバナンスや管理の課題でよく知られています。その中には以下のようなものが含まれます：
    - >  1. While the contributions of open-source contributors are recorded, recognition is hard to track/trace be- cause contributions are not clearly valued in relation to higher-level ob jectives. This reduces motivation and sustainability.
    - > オープンソースの貢献者の貢献は記録されますが、貢献が高次の目的に関連して明確に評価されていないため、認識が追跡・追跡しにくいです。これにより動機付けと持続可能性が低下します。
        - コミットログがあってもな〜ということ
        - たくさんコミットしたりプルリクエストしたりイシューを書いたりしたら貢献なわけではない
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>仕事一般に通じるな。やったことをいくら集めても、「で、会社にとって利益になったのか」はよくわからない
    - >  2. While contributions to open source projects are gen- erally open and participatory, management (often called “maintenance”) of them usually falls in the hands of a “benevolent dictator for life”, contradict- ing the underlying democratic values and leading those who dissent to “fork” projects, fragmenting ef- forts.
    - > オープンソースプロジェクトへの貢献は一般的にオープンで参加型ですが、その「管理（通常は「生涯の慈悲深い独裁者」と呼ばれます）は、しばしば根底にある民主的な価値に反して、数人の手に渡ります。これに反対する人々はプロジェクトを「フォーク」し、努力を分断します。
        - オープンソースプロジェクトにみんな参加してね、誰でもプルリクエストできるよ、という「民主的な価値観」を持ってるけど、結局そのマネジメントは「[[慈悲深い独裁者]]」による独裁制(や寡頭制)になるよね、という話
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> そう、慈悲深い独裁者によってオープンソースはなりたっている。
            - それが生み出す結果が悪いかどうかはさておき。個人的には「OSSにおいては、有能な個人による独裁制が良いパフォーマンスを出してきたよなぁ、結局有能な個人による独裁制が最良の統治方法なのかも」という気持ちが捨てきれない
            - もちろん「今まで独裁制によって良い結果を出したOSSがいくつもある」ということは、論理的には「民主的メカニズムによってより良い統治ができる可能性」を否定しない
            - また、フェーズによって異なる可能性もある、プロジェクト初期には一人の独裁者がバリバリコードを書くべきで、その後その人のテンションが下がってきた時に民主的メカニズムが有益になる可能性

            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>「新しい民主主義」っていわれるとイメージがぼんやりするけど、新しいオープンソース運営方法っていわれると、なんかはっきりする、気がする。
                - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 今の民主主義がわかりにくいのは国政などの「組織がデカくて問題が身近じゃないもの」に対して「自分の代わりに考える人を選ぶ」という間接民主制だからという側面もある。オープンソースとか町内会とかだと問題が身近だよね
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>おお、町内会をオープンソース的にやろう、ってことか！！なんかわかりやすい。
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>逆に考えると間接民主主義的なOSS運営も理論的には存在するのか
                - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 「コミッターを選挙で選びます」ってやればそうなる

        - 独裁的統治に不満がある時、フォークできる
            - フォークできるのはOSSの長所
            - 一方で、フォークによって人々の努力は分散してしまう
            - (統治方針の異なるプロジェクトがあれば人々の努力が分散するのは仕方ない気もする)
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 今はおかしければフォークして、前のは不人気になる。
                - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>そう、[[フォークできるなら政治は不要]]、[[すべてのフォークは存在を許され、どのフォークに関心を持つかは周囲のコミュニティに委ねられる]]、[[誰も強制されない]]
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> Wikipediaでも同じ仕組みが適する気がする
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> OSSはフォークできるっていうのが必殺技なんだよなあ。町内会や国政だと、革命するってこと？もっと平和的に競争できないのかなあ。
                - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>国政だと革命みたいになっちゃうけど、地方自治体レベルでIssuesの重みづけをどうしようかという話だと各自治体の裁量の範囲なので各自治体が試行錯誤できるし、新しいチャレンジに積極的な市長のいる市とかで直接民主制が導入されて、それで「この市はいいな」となると人口流入になる
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> なるほど、地方行政はそこそこ競争されているよ、と。
            - 追記: [[社会制度をフォークする]] by Audrey Tang
                - 実際に[[g0v]]などでフォークしている
                - あと[[民主主義はリアルタイムシステムへと進化する必要がある]] [“Democracy needs to evolve into a real-time system” - Vodafone Institute](https://www.vodafone-institut.de/aiandi/democracy-needs-to-evolve-into-a-real-time-system/) においても「Ethereum基盤の上で作られた社会制度はデータもコードも公開されるのでフォークしやすくなり、どのフォークを選ぶかで事後的に正当化される」という趣旨のことを言ってる([[social inovation legitimates governance]])
    - >  3. Worse, the inability to leverage distributed participation to assist in management makes projects large burdens on maintainers, who begin projects with high motivation but are forced to maintain their quality for years after, forcing them to triage increasing volumes of contributions of dubious quality with little community support.
    - > さらに悪いことに、分散した参加を管理に活用することができないため、プロジェクトは保守者に大きな負担となります。彼らは最初は高いモチベーションでプロジェクトを始めますが、その後何年もの間、質を維持することを強いられます。これにより、コミュニティのサポートが少ない中で疑わしい品質の寄稿が増えていくことに対処する必要があります。
        - 保守めんどい問題
    - >  4. Especially as they grow and are more broadly used, potential directions for improvement of a project grow exponentially and there is typically little clar- ity on what improvements are most needed by users, leading to projects that have too many features and insufficient usability.
    - > 特に成長し、より広く使用されるようになると、プロジェクトの改善のための潜在的な方向性が指数関数的に増加し、ユーザーにとって最も必要な改善が何であるかについて通常はほとんど明確ではありません。これにより、多くの機能と不十分な使いやすさを持つプロジェクトが生じます。
        - 知名度が上がると「あの機能がない」「この機能をつけろ」的なことを言い出す人が湧いてくる
        - そして枝葉の機能追加の方が貢献が容易なのでうかうかしてるとそういうプルリクエストがどんどんきてしまう
            - それをレビューしてマージするべきかどうか意思決定する負担が少数のコミッターに集中してうえーとなる
            - 一方で、レビューしないとプルリクエストを送った側は「せっかく貢献したのに放置されている」と感じてやる気が減退する
        - どんどん採用していくと[[ボタンが大量についたテレビのリモコン]]みたいに、ゴテゴテと微妙な完成度のオプションがついた汚いソフトウェアになる
    - >  By offering greater clarity and empowerment to con- tributors, plural management can help founders to slowly transition management authority to those who prove their merit by contributing code, diligence, or support in a way that is measurably valuable to the community in question. Since the model is lightweight, iterative, and self-directed, it is well suited for commonly used agile environments and tools of the kinds often used by open-source communities. Consider the most popular open-source hosting plat- form GitHub. For any given project there is a reposi- tory of code, set up by an administrator or maintainer, within which any contributor is listed as a member. At- tached to this repository is an Issues section (extremely similar to our described issue board, just without any ex- plicit priorities assigned numerically). Anyone on GitHub can create a contribution on this board in the form of a ‘pull request’ (shorted to PR) that aims to address one or more outstanding issues. After the pull request is dis- cussed in a comment section, the community can decide whether to accept or reject it, and in turn, maintainers can add or ‘merge’ the contribution into the repository. Using Plural Management, with minimal changes to workflows, any maintainer or administrator could set priority tags on GitHub, associate a price in credits, and in turn drive more contributions to their repository as a first step in eventually improving their bus factor from the low average of two (Metabase, 2022).
    - > プルーラル・マネジメントが貢献者により大きな明確さと権限を提供することで、創設者はコードの提供、注意深さ、またはコミュニティにとって計測可能な価値ある方法でのサポートによって実績を証明した人々に管理権限を徐々に移行する手助けをすることができます。このモデルは軽量で反復的で自己指導的であるため、オープンソースコミュニティによってよく使用されるアジャイルな環境やツールに非常に適しています。最も人気のあるオープンソースホスティングプラットフォームであるGitHubを考えてみましょう。任意のプロジェクトには、管理者またはメンテナーによって設定されたコードのリポジトリがあり、その中に任意の貢献者がメンバーとしてリストされています。このリポジトリにはIssuesセクションが付随しており（我々が説明した問題ボードに非常に似ていますが、数値で明確に割り当てられた優先順位はありません）、GitHub上の誰でもこのボードに‘プルリクエスト’（PRと略されます）という形で貢献を作成でき、それは一つ以上の未解決の問題に取り組むことを目的としています。プルリクエストがコメントセクションで議論された後、コミュニティはそれを受け入れるか拒否するかを決定でき、その結果、メンテナーは貢献をリポジトリに追加または‘マージ’することができます。プルーラル・マネジメントを使用して、ワークフローに最小限の変更を加えることで、任意のメンテナーや管理者がGitHub上に優先順位タグを設定し、クレジットで価格を関連付けて、リポジトリへの貢献を増やし、最終的には平均2の低いバス係数（Metabase、2022年）を改善するための第一歩を踏み出すことができます。
        - GithubのIssuesに優先順位がついてないからどれが大事なのかわかんないよねという話
            - ラベルで重要度を表現することは可能だが、誰でも追加できたらみんな自分の書いたイシューに「重要！」って付けるから機能しなくなる
            - では少数の「メンテナー」が、パーミッションレスにどんどん有象無象から送られてくるイシューを全部レビューして適切に優先順位づけするのか、というと:
                - 作業負担の集中の問題
                - 権限の集中の問題
        - 安心して任せることのできる人は希少なリソースであり、人間には家庭の事情とかがあるので急に活動できなくなったりする
    - >  It’s worth noting for the general case that, while contributions are typically code, anything could be made a PR. For example, if someone were to be appointed to the social media manager for a project, an issue stating the need for a social media manager could be made, and when someone is to be appointed, a simple PR adding the name of the person to the community notes could be made by the new social media manager. If the community votes to approve this new role, the social media manager will now be rewarded with additional management credits reflect- ing their new role.
    - > 一般的なケースとして注目すべき点は、貢献は通常コードですが、何でもPRにすることができるということです。例えば、誰かがプロジェクトのソーシャルメディアマネージャーに任命される場合、ソーシャルメディアマネージャーが必要であることを示す問題を作成し、任命されると、新しいソーシャルメディアマネージャーがコミュニティノートにその人の名前を追加するシンプルなPRを作成できます。コミュニティがこの新しい役割を承認すると、ソーシャルメディアマネージャーは、その新しい役割を反映した追加の管理クレジットで報酬を受けることになります。
        - なんでもプルリクにする



# 2.2 A succinct example of use
- 具体例
- > A tangible example of the use of plural management be- yond the usual open-source context is the plurality book, an open, git-based experiment around collective author- ship. Initiated by E. Glen Weyl and Audrey Tang, 50 members around the world have contributed to the book, Plurality: The Future of Collaborative Technology and Democracy without any expectation of reward. Using the plural management protocol, this project seeks to tran- sition ownership over future improvements to the book incrementally, including updates to content, translations, and further links to relevant materials. Over time, those who have contributed most meaningfully will therefore help guide not just the book but the field of research itself.
- > プルーラル・マネジメントの使用例として、通常のオープンソースの文脈を超えた具体的な例が「Plurality Book」です。これは集団著作を巡るオープンでGitベースの実験で、E.グレン・ウェイルとオードリー・タンによって開始されました。世界中の50人のメンバーが、報酬を期待せずに「Plurality: The Future of Collaborative Technology and Democracy」という本に貢献しています。プルーラル・マネジメント・プロトコルを使用して、このプロジェクトは本への将来的な改善、コンテンツの更新、翻訳、関連資料へのさらなるリンクなど、徐々に所有権を移行することを目指しています。時間の経過とともに、最も意味のある貢献をした人々が、本だけでなく研究分野自体の指針となることが期待されます。
    - Plurality Bookについて詳しく知りたければ[/plurality-japanese/初めに読んでね](https://scrapbox.io/plurality-japanese/初めに読んでね)を参照
    - 僕もこの一員になりたくて活動してて、一応参加は認められてる
        - まだクレジットは獲得してないので意思決定に参加できてはない
- > Consider an undergraduate student of political econ- omy at a lesser-known university. Seeing a typo, she opens up an issue and submits a PR. This action does not net many credits during voting, but the small number she is given allows her to begin participating in priority setting. Motivated, she continues searching for opportuni- ties to contribute and recognizes that an outstanding issue around additional content for a chapter could benefit from her thesis work. She submits a PR on the board to add a number of key references that get cited in the book and is rewarded with significant credits.
- > 例えば、あまり知られていない大学の政治経済学の学部生を考えてみましょう。彼女はタイポを見つけ、問題を提起し、PRを提出します。この行動は投票中に多くのクレジットを獲得するわけではありませんが、彼女が与えられた少数のクレジットによって優先順位設定に参加することができます。彼女はモチベーションを持って貢献の機会を探し続け、ある章の追加コンテンツに関する未解決の問題が彼女の論文作業から恩恵を受けることを認識します。彼女は、本で引用されるいくつかの重要な参考文献を追加するためにボードにPRを提出し、かなりのクレジットで報酬を受けます。
    - The Plurality Bookに、あんまり我田引水じゃない世界の人にちゃんとメリットがある形で日本の事例とかを提供できるといいなと思う
- > Given the existing challenges of inclusion within the post-secondary context, without the permissionless and community-judged power structure afforded by plural management such a student may never have had the op- portunity to participate in such work (Gvozdanović and Maes, 2018).
- > 後期教育の文脈における既存の包摂の課題を考えると、プルーラル・マネジメントによって提供される許可不要でコミュニティが判断する権力構造がなければ、このような学生がそのような作業に参加する機会は決してなかったかもしれません（グヴォズダノビッチとマエス、2018年）。
    - 一貫したストーリーを作ることは難しいが、ストーリーに対して具体的事実の例を付与することは比較的コントリビューションしやすい

# 3 Model details
- > The plural management protocol describes two key ac- tivities: a prioritization subsystem and an approval sub- system. These subsystems exist jointly and constitute a broader organizational structure, where individuals earn management credits that can be used to perform actions. These credits can be initially distributed when an organi- zation is established and are naturally distributed to new members as they participate (in effect lessening the con- trol of founders over time). The credit can be stored in any simple ledger that can be amended over time when interacting with the protocol.
- > プルーラル・マネジメント・プロトコルでは、主に二つの重要な活動、すなわち「優先順位付けサブシステム」と「承認サブシステム」について説明されています。これらのサブシステムは共存し、より広範な組織構造を構成しています。この構造の中で個々の人々は管理クレジットを獲得し、これらのクレジットを使用して行動を実行することができます。これらのクレジットは、組織が設立された際に初めて配布され、参加する新メンバーに自然に分配されます（事実上、創設者のコントロールを時間とともに減少させる効果があります）。クレジットは、プロトコルとの対話によって時間とともに修正可能な任意のシンプルな台帳に保存することができます。
    - 台帳がブロックチェーンである必要は全然ないよ、ということ
        - ソースコードやイシューの管理にGithubを使ってる時点で情報が集約されてるからね、マネジメントシステムだけ分散しても意味がない
        - もちろん、イシューの管理なども含めてオンチェーンで分散的にやろうとチャレンジしてる人もいるだろうけど、この論文が解決したい問題はイシューの情報が特定のサービスに集約してるところじゃないってこと
- >  There are many additional considerations surrounding the sharing, control, and visibility of these management credits. For example, should an organization dynamically run on management credits to make the score of every member public (in essence creating a ranking of implicit authority)? Should individuals be able to directly send management credits to another member (this would ease the setup challenges for new members and allow old mem- bers to gracefully leave, but could also reduce meritocracy and result in off-the-books gambling or scheming)? We re- turn to these open questions in our conclusion.
- > これらの管理クレジットの共有、コントロール、可視性に関しては多くの追加的な考慮事項があります。例えば、組織が管理クレジットで動的に運営され、すべてのメンバーのスコアを公開する（本質的に暗黙の権威のランキングを作成する）べきか？ 個々の人々は他のメンバーに直接管理クレジットを送ることができるべきか（これにより新メンバーのセットアップの課題が軽減され、古いメンバーが優雅に去ることができますが、メリトクラシーが減少し、オフ・ザ・ブックの賭けや策略が行われる可能性もあります）？ これらの未解決の問題について、我々は結論で再び取り上げます
    - [[メリトクラシー]]が減少してオフザブックの策略の可能性がある、というのは要するに「管理クレジットをリアルマネーで売ってくれ」という交渉が成立しちゃうこと
        - 金でクレジットが買えるなら、金をたくさん出せる人がコントロールする力を得ることができる
        - しかもその金はプロジェクトの公共プールに入るのではなく、個人のポケットに入る
        - 一方で個人が貢献して管理クレジットを得ても、それを現金化する手段がないなら生活に余裕のある人しか参加できないよな
        - 議論は後であると思うので先に進む

# 3.1 Prioritization
- ![image](https://gyazo.com/7f55cdbd7e90c02ee08e025888d5d6ad/thumb/1000)
    - すべてのイシューはボードに表示され、メンバーはマネジメント・クレジットを消費することで、課題の優先順位を設定することができる。([[Quadratic Funding]]の仕組み)
    - 各メンバーが$P_i$の消費をしたら優先度は
    - $\left(\sum_i \sqrt{P_i}\right)^2$
        - になる
    - 大口のクレジット保有者は、マッチングファンドを追加できる。
    - ある問題に対処するために貢献が行われた場合、優先度への投票クレジットとマッチングクレジットは凍結され、貢献投票が可決された場合に貢献者に割り当てられる。
- > The first subsystem to consider is the priority-setting step via the issue board. Every major task or strategic challenge should be assigned an issue on the board, simi- lar to how most open-source projects operate in GitHub.
- > 最初に考慮すべきサブシステムは、問題ボードを通じての優先順位設定ステップです。各主要なタスクや戦略的な課題は、GitHubでのほとんどのオープンソースプロジェクトが行うように、ボード上に問題として割り当てられるべきです。
- よくあるIssuesみたいなやつ
- >  Each member can spend a portion of their management credits on priority setting. This is done dynamically and members can add or withdraw credits from each issue at any time. For each member who sets a priority to an issue by assigning Pi credits, we sum over the square roots of their priority and take the total square to find the total issue priority. Hence, the quadratic priority for issue j is (equation) . This is exactly akin to quadratic funding, from which we further draw on the idea of a matching fund. A matching fund is generated from credits used in voting or further increased by a large man- agement credit holder (such as an early founding member) who may choose to assign funds as a matching pool to dis- tribute to new contributors as incentives to join.
- > 各メンバーは、優先順位設定のために自分の管理クレジットの一部を使うことができます。これは動的に行われ、メンバーはいつでも各問題にクレジットを追加または引き出すことができます。各メンバーがPiクレジットを割り当てることで問題に優先順位を設定する場合、彼らの優先順位の平方根を合計し、その合計の平方をとることで問題の総優先順位を見つけます。したがって、問題jの二次優先順位は（方程式）です。これは二次資金調達に完全に類似しており、そこからさらにマッチングファンドのアイデアを引き出します。マッチングファンドは投票で使用されるクレジットから生成されるか、または大きな管理クレジット所有者（たとえば、初期の創設メンバー）が新しい貢献者に参加するインセンティブとしてマッチングプールとして割り当てることを選択することによって増加することがあります。
    - $QP_j = \left(\sum_i \sqrt{P_i^j}\right)^2$
    - これはまあ[[Quadratic Funding]]ですね
    - そこからマッチングファンドの概念が自然に出てくる
        - 特定のissueではなく、全体に対してクレジットを払うことができて、それの分配に関しては他の寄付によって決まる
- >  In reality, a matching fund may not always have sufficient credits to fully subsidize the quadratic priority. To address this, the total contribution payout (CP) is adjusted proportionally to the matching fund2.
- > 現実には、マッチングファンドには常に二次優先順位を完全に補助するための十分なクレジットがあるわけではありません。これに対処するため、総貢献支払い（CP）はマッチングファンドに比例して調整されます。
    - 脚注に数式が書いてある、今回はスキップ
- >  When a contribution is made to address an issue, the payout should be frozen for that issue3. The contribution then goes to a vote as below. If the vote fails, the issue simply comes back to the board for other contributions to be suggested.
- > 問題に対処するための貢献がなされた場合、その問題の支払いは凍結されるべきです。その後、貢献は以下のように投票にかけられます。投票が失敗した場合、問題は単にボードに戻り、他の貢献が提案されます。
    - 「いつでも出し入れできる」という状態から、プルリクが来た段階で一旦出し入れ不能になる
    - それから評価のプロセスが走る
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 投票のやり直しができるのは面白い！しかも投票が終わらなくても、現状どうなっているか見れる。
- >  Only contributions addressing existing issues are re- warded. To receive a reward for an unsolicited contribu- tion, a contributor would need first to submit an issue and persuade the community it is worth addressing; given the quadratic nature of the matching, an individual adding an issue and contributing to it themselves can never be re- warded more than they contribute to the issue in credits. Thus an individual must persuade others of the value of their contribution in order to receive a net reward.
- > 既存の問題に対処する貢献のみが報酬を受けます。依頼されていない貢献に対して報酬を受け取るためには、貢献者はまず問題を提出し、コミュニティにそれが対処する価値があると説得する必要があります。マッチングの二次的な性質を考えると、個人が問題を追加し、自分でそれに貢献しても、問題に対するクレジットの貢献以上の報酬を受けることは決してありません。したがって、個人は自分の貢献の価値を他者に説得することで、正味の報酬を受け取る必要があります。
    - 自分で作って「これが必要だ！」とプルリクエストしただけでは報酬クレジットの支払いを自分がやるので得にならないってこと
    - まず「こういう貢献が必要だと思うんだけど、どう？」と提案して、他の人からの賛同を集める必要がある
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> じゃあプルリクを手元で作っている間は、公表しない方が良いと判断する人もいるな

# 3.2 Approval
- ![image](https://gyazo.com/4c3bcfebd114bd03b72b4764af37b320/thumb/1000)
    - > 貢献に関する投票は、どのメンバーも賛成または反対にコストv^2で強さvの投票を行うことができるところで行われます。
    - > これは標準的な単一問題の二次投票です。
        - シンプルな[[Quadratic Voting]]だよね、ということを言ってる
    - > 組織の管理者は、貢献の成功の可能性を予測するためにメンバーにインセンティブを与えるために、問題の報奨金から資金を割り当てることを選択できます。
    - > これは正しい予測に対する報酬として、少額のクレジット所有者が組織全体のニーズを理解し、貢献に対する適切な調査を行うことを奨励します。
    - > 予測者は2vの報酬を受け取り、管理者はパラメータKを設定することによって、投票のコストを予測に対して低減することができます。
- > Once a contribution is made, it goes to a vote. Any member with management credits can vote, and in line with the quadratic voting approach, it will cost v2 credits for a vote of strength v. Any individual can vote for or against, where votes against can be treated at a negative value of v for the sake of determining the outcome. As with any quadratic vote, there should be an appropriate time to allow for the vote to occur and the verdict after this time is simply the sum of the votes. In the simple case, all of the funds put into the issue during priority setting go to the contributor. All the credits used by members during voting flow directly into the general matching fund for priority setting4 .
- > 貢献が行われると、それは投票にかけられます。管理クレジットを持つどのメンバーでも投票でき、二次投票アプローチに沿って、強さvの投票にはv^2のクレジットが必要です。個々の人は賛成または反対に投票でき、反対票は結果を決定するために負の値vとして扱われます。他の二次投票と同様に、投票が行われ、結果が出るまでに適切な時間が設けられるべきです。この時間の後の判定は単に投票の合計です。簡単な場合では、優先順位設定中に問題に投じられたすべての資金は貢献者に行きます。投票中にメンバーが使用したすべてのクレジットは、優先順位設定のための一般的なマッチングファンドに直接流れます。
    - 意思表示に使われたクレジットはマッチングプールに入る
- >  This act of simply voting is costly, meaning that mem- bers can spend earned trust to exert authority and influ- ence the direction of the organization or project. As a result, an early member of the community with few cred- its would find it proportionally quite costly to sway a vote relative to their means. This further means that members with few management credits have no incentive to do due diligence on contributions (often a significant workload) to determine their fit for the project.
- > 単に投票する行為はコストがかかるため、メンバーは獲得した信頼を使って権威を行使し、組織やプロジェクトの方向性に影響を与えることができます。その結果、クレジットが少ない初期のコミュニティメンバーは、自分の手段に比べて投票を揺さぶることが比例してかなりコストがかかることになります。これはまた、管理クレジットが少ないメンバーがプロジェクトに適合するかを判断するための貢献（しばしば重要な作業負荷）に対して適切な調査を行うインセンティブがないことを意味します。
    - 管理クレジットが少ないメンバーは何か意見を出しても投票があまり動かないので、レビューに貢献するインセンティブがない
- >  In order to incent lower authority members to partic- ipate in the vote and provide a signal of quality for the contribution, organization administrators can reward an additional prediction step by voters. Administrators will choose a parameter K that reduces the cost of voting rel- ative to prediction. The cost of voting will be Kv2 if no prediction of a correct vote is made, or Kv2 +v if a wager of v is made alongside the vote. The payouts for these correct predictions will come from the contribution pay- out and can be seen as a processing fee to incent analysis of the contribution.
- > より権限の低いメンバーが投票に参加し、貢献の品質に関するシグナルを提供するために、組織の管理者は投票者に追加の予測ステップを報酬として提供することができます。管理者は、予測に比べて投票のコストを減らすパラメータKを選択します。正しい投票の予測が行われていない場合の投票コストは$kv^2$となり、投票と同時にVの賭けが行われた場合$kv^2+v$となります。これらの正しい予測に対する報酬は、貢献の支払いから来るもので、貢献の分析を促進するための処理手数料と見なすことができます。
    - そこで予測市場のアプローチを導入する
    - 正しく予測できればボーナス
- >  Predictors can choose to make no prediction without cost or wager exactly v additional credits that the outcome they voted for will succeed5 for a payout of 2v6. For large values of K (e.g., one or greater), voting would only be profitable for exceptionally small numbers of credits due to the quadratic cost of voting (although one can still mini- mize their losses by wagering v credits when the likelihood of passing is believed to be greater than 12 ). When K = 0, there is no cost to voting and one should (if one is risk- neutral) wager the maximum credits if they believe their vote will pass. This setting of K = 0 should be avoided and indeed Theorem 3 will show that K can and should be set high enough not to reduce the contribution payout more than expected. In general, administrators can learn over time what choices of K are needed to incent different mixtures of behavior.
- > 予測者は、予測せずにコストなしで参加することを選択するか、自分が投票した結果が成功するというvのクレジットを賭けることができます。(5) この場合、正しい予測に対して$2v$の報酬が得られます。(6)
- >  Kの値が大きい場合（例えば、1以上）、投票の二次的なコストのために、非常に小さなクレジット数に対してのみ投票が利益をもたらすことになります（ただし、合格する可能性が半分以上だと信じる場合にvのクレジットを賭けることで損失を最小限に抑えることができます）。K = 0の場合、投票にはコストがかかりませんので、リスクニュートラルな場合、自分の投票が通ると信じる場合は最大のクレジットを賭けるべきです。このK = 0の設定は避けるべきであり、実際に定理3では、Kは貢献支払いを予想以上に減少させないほど十分に高く設定することができ、そしてすべきであることが示されます。一般的に、管理者は時間をかけて、異なる行動の混合を奨励するために必要なKの選択を学ぶことができます。
    - 調整できるパラメータがあり、行動がよく混合されるように調整することが必要ということ
    - Footnote
        - > (5) Individuals can only be in the direction of their vote and in an amount capped by their vote, as this incents approximately truthful predictions from the logic of quadratic scoring rules (Selten, 1998).
        - > 個々の人々は自分の投票の方向と投票によって上限が設定された金額のみで賭けることができます。
        - 自分が正しいと思っている方向にしか掛けられない
        - > (6) Given no hedging and a quadratic vote, we will see in Theorem 1 that given the ability to wager any number between 0 and v, it is always optimal to wager v when you believe the probability of success is greater than a half.
        - >  ヘッジがなく二次投票を行う場合、0からvまでの任意の数を賭ける能力が与えられた場合、成功の確率が半分以上であると信じる場合は常にvを賭けるのが最適です。
- >  An important aspect of the mechanism is that this prediction reward is only positive for small votes. Due to the squared cost of voting, large votes with high impact will not ever be profitable for reasonable non-zero values of K. This is an important property such that existing authority figures with large sums of management credits are not rewarded for understanding the community preferences and rewards go to those who are seeking to increase their influence from modest means.
- > このメカニズムの重要な側面は、この予測報酬が小さな投票に対してのみプラスになることです。投票の二次的なコストのために、大きな影響を持つ大きな投票は、Kの合理的な非ゼロ値に対しては決して利益をもたらしません。これは重要な特性であり、多額の管理クレジットを持つ既存の権威者がコミュニティの好みを理解するために報酬を受け取らず、謙虚な手段から影響力を増やそうとする者に報酬が行くことを保証します。
    - 多額の管理クレジットを持つ既存の権威者には「コミュニティの好みを理解する」インセンティブを得る必要がないから

4 Analysis of protocol properties
- 4.1 Mixed utility analysis
- ここは今回はスキップ

# 5 Open questions
- > 5 未解決の問題

- > Plural Management, while versatile in theory, encoun- ters practical challenges in diverse organizational scenar- ios. Its adaptability to both modern, open-source en- vironments and traditional hierarchical structures raises questions about its real-world efficacy and implementa- tion strategies. This section probes into these nuances, inviting deeper exploration and collaborative research to navigate the complexities of applying Plural Management in varying contexts.
- > プルーラル・マネジメントは理論上は多用途ですが、多様な組織環境において実践上の課題に直面します。現代のオープンソース環境と伝統的な階層構造の両方に適応する能力は、その実世界での効果と実施戦略についての疑問を提起します。このセクションでは、これらのニュアンスに探りを入れ、異なる文脈でプルーラル・マネジメントを適用する複雑さをナビゲートするために、より深い探求と協力的な研究を求めます。

- > (1) In refining Plural Management’s quadratic vot- ing, it’s crucial to recognize and strategically address the potential for collusion within homogeneous socio-cultural groups in organizations, considering dimensions like location, department, role, and origin. Building on foun- dational research (Miller et al.), this approach advocates for a nuanced mechanism that actively discounts the disproportionate influence of these groups. Such a system would not only enhance fairness but also promote a gen- uinely diverse and representative decision-making process, ensuring that no single faction within the organizational tapestry exerts undue control, thus aligning more closely with the realities of complex organizational structures.
- > (1) プルーラル・マネジメントの二次投票を洗練させるには、組織内の均質な社会文化的グループ内での共謀の可能性を認識し、戦略的に対処することが重要です。地域、部門、役割、出身などの次元を考慮して、これらのグループの過大な影響力を能動的に割引くような洗練されたメカニズムを構築することが提案されています（ミラー他の基礎研究に基づく）。このようなシステムは公平性を高めるだけでなく、真に多様で代表的な意思決定プロセスを促進し、組織内の単一の派閥が不当なコントロールを行使することがないようにし、複雑な組織構造の現実により密接に整合させます。
    - 特定の社会的グループが強い力を持つことを防ぐために、各種の属性を見て自動的に割り引こうという話
    - 例えばアメリカだと白人男性ばかりが意思決定を握っていると良くないよねという話になる
    - 日本でも経営陣が「日本人の男性のだいたい似たような年齢の人ばかり」ということに批判が向くようになってきた
    - そういう個人の属性に基づく多様性の確保がどの程度実際のパフォーマンスを増やすことに有益かは色々議論はあるが、まあ計測しにくい「考え方の多様性」を増やすアクションはやりにくいから計測しやすい多様性をまず強化してしまえばいいんじゃないかという考え方
        - [https://dhbr.diamond.jp/articles/-/4627](https://dhbr.diamond.jp/articles/-/4627)
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 白人ばかりがポイントを集めるわけではなさそうだけど・・・。
- > (2) Can we extend this approach to create a multi- layered decision-making framework within organizations? This would involve developing independent yet intercon- nected systems for various organizational strata, such as departments or teams, each with its own tailored voting mechanism. Such a model could facilitate more localized and relevant decision-making, while maintaining coher- ence with the broader organizational objectives. This ap- proach merits exploration for its potential to harmonize individual group dynamics with the overall organizational structure.
- > (2) 組織内で多層的な意思決定フレームワークを作成するために、このアプローチを拡張することができるか？ これには、部門やチームなどの組織の各層に対して、独立していても相互に連結されたシステムを開発し、それぞれに合わせた投票メカニズムを持たせることが含まれます。このモデルは、より地域化された関連性のある意思決定を促進し、広範な組織目標との整合性を維持することができます。このアプローチは、個々のグループダイナミクスを全体的な組織構造と調和させる潜在能力について検討される価値があります。
    - これは結局のところ組織全体の解くべき課題を一つのIssuesにすることなんてできないんじゃない？ということ
    - 例えばインサイダー情報であったり、人事部が知った従業員個々人のセンシティブな情報だったりを全社員公開のIssuesに置くことができるかどうか
    - 別に「とにかく階層構造が悪だから解体しよう！」と言ってるわけではないので、入れやすいところに(個々の部署内とかで)導入した上で、組織全体のIssuesとうまいことつなぐ方法があるといいなという話
    - 個人的には、そもそも非公開情報とかがなくてもある程度大きな組織のIssuesは情報洪水が起きて「全部見て優先順位づけをする」なんてことはできないだろと思う
- > (3) While rational actors may be further motivated by extrinsic incentives, their overuse has the potential to cre- ate what is referred to as ’motivation crowding’ in which intrinsically driven contributors are discouraged from par- ticipating in a project (Frey and Jegen, 2000). While management credits are not by default monetary, the decision to distribute such rewards based on them must therefore be made in the context of existing organizational cultures.
- > (3) 合理的な行動者は外的インセンティブによってさらに動機付けられる可能性がありますが、その過度の使用は、内発的に駆り立てられる貢献者がプロジェクトへの参加を抑制される「モチベーションの混乱」を生み出す可能性があります（フレイとイェゲン、2000）。管理クレジットはデフォルトでは金銭的ではありませんが、それに基づいて報酬を分配する決定は、既存の組織文化の文脈で行われる必要があります。
    - 管理クレジットは金銭ではないが、その情報を金銭的報酬につなげる話
    - 逆にモチベーションの[[アンダーマイニング]]になる可能性もある
        - [モチベーションのクラウディングアウト - Wikipedia](https://ja.wikipedia.org/wiki/%E3%83%A2%E3%83%81%E3%83%99%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%82%AF%E3%83%A9%E3%82%A6%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%A2%E3%82%A6%E3%83%88)
    - 個人的には、金銭でドライブされる活動と金銭でないものでドライブされる活動は本質的にモチベーションの仕組みが違うので同一視しないほうがいいと思う
- > (4) The transparency of status hierarchies within orga- nizations, as is often studied with respect to salaries, can have meaningful impacts on contributor behavior (Cullen, 2023). While this can improve employee outcomes, it can also reduce internal collaboration and potentially harm long-term organizational objectives. Given its ease of im- plementation, plural management provides a sandbox for comparing and contrasting how public or private records of credits impact performance within a group.
- > (4) 組織内のステータス階層の透明性は、しばしば給与に関連して研究されますが、貢献者の行動に重要な影響を与える可能性があります（カレン、2023）。これにより従業員の結果が改善される可能性がありますが、内部協力が減少し、長期的な組織目標に悪影響を及ぼす可能性もあります。実施が容易であるため、プルーラル・マネジメントは、クレジットの公開または非公開記録がグループ内のパフォーマンスにどのような影響を与えるかを比較検討するための実験場を提供します。
    - このシステムでは階層組織でのステータス階層の代わりに管理クレジットを使う
    - その量を可視化することは良いことなのか悪いことなのか
    - 個人的には、全社クレジット一種類で人間をランクづけするとネットのゲームのスコアランキングと同じで上位の少数の人以外はやる気がなくなると思う
        - そういう意味でも会社の中にいくつものIssuesボードがある状態が好ましいかもね
        - 複数部署兼任をすると活動の全体が見えにくくなるわけだが、貢献の全体を給与査定者に伝える上で「今年はメインの組織での活動は減ったが、それ以上にクロスセクションのチームでこんなに貢献を生み出したんだ」と説明できるようになる
- > (5) Currently, individuals cannot directly send man- agement credits to another member, as a way to prevent off-book trading of management credit which could result in a market price for management authority. This helps prevent the financialization of management authority, and makes certain behaviors difficult or impossible. For example, if a founder wants to bring in a new member quickly to provide authority, they cannot directly send credits and must conduct elaborate PR rewards for this contributor that are voted on by the whole community (in some sense also preventing nepotism). Further, if a member wants to leave, they cannot transfer credits to others quickly aside from putting all credits in a matching fund. Future re- search into the implications of enabling direct trading is important before incorporating it.
- > (5) 現在、個々の人々は他のメンバーに直接管理クレジットを送ることができません。これは、管理クレジットのオフブック取引を防ぐ方法として設計されており、これにより管理権限の市場価格が生まれる可能性があります。これは管理権限の金融化を防ぎ、特定の行動を困難または不可能にします。例えば、創設者が迅速に新しいメンバーを権威を持たせるために招き入れたい場合、直接クレジットを送ることができず、全コミュニティによって投票されるPR報酬を行う必要があります（ある意味で縁故主義も防ぐ）。さらに、メンバーが離れたい場合、マッチングファンドにすべてのクレジットを入れる以外に、迅速に他の人にクレジットを移すことができません。直接取引を可能にする影響に関する今後の研究は、それを組み込む前に重要です。
    - 個人間のクレジット送金が可能であるべきか否か
    - 「縁故主義も防げる」が、結局それ自体が悪なのではなく「組織外の人間関係によって組織に新しく来た特定の人に、他の新しい人よりと異なった力を与えることが妥当か」ということになる
    - 個人的には行動の選択肢はあったほうがいいと思うな
- > (6) Deciding when and how to promote an employee is a mission-critical question across organizations. How- ever, in large hierarchies employees are often promoted based on their performance in an existing role rather than their capacity to set high-level priorities leading to bad management (Benson et al., 2018). An evaluation of the effects plural management has on promotion results, for example by evaluating how top contributors perform in administrator roles, would be helpful.
- > (6) 従業員の昇進をいつ、どのように決定するかは、組織全体でのミッションクリティカルな質問です。しかし、大規模な階層組織では、従業員はしばしば現在の役割のパフォーマンスに基づいて昇進され、高レベルの優先順位を設定する能力ではなく、悪い管理につながることがあります（ベンソン他、2018）。プルーラル・マネジメントが昇進の結果に及ぼす影響を評価すること、例えば上位の貢献者が管理者の役割でどのようにパフォーマンスを発揮するかを評価することは有用です。
    - これも給与の査定や階層的ステータスと似た話で、このシステムの外の組織構造における昇進にこのシステムの情報を使うかどうかの話題
    - 次も関連
- > (7) The current design of plural management is fo- cused on a single organization, community, or project. Many large organizations are constructed as many sub- organizations working together in the form of depart- ments, units, or project teams. Future work could exam- ine the use of plural management to create multiple par- tially nested versions that allow management authority to be exercised within a sub-organization, while still allowing individuals to climb the ranks of larger workplaces.
- > (7) 現在のプルーラル・マネジメントの設計は、単一の組織、コミュニティ、またはプロジェクトに焦点を当てています。多くの大規模な組織は、部門、ユニット、またはプロジェクトチームの形で一緒に働く多くのサブ組織として構築されています。今後の作業では、プルーラル・マネジメントを使用して、サブ組織内で管理権限を行使しながら、個人がより大きな職場の階級を登ることを可能にする多数の部分的にネストされたバージョンを作成することが検討されるかもしれません。
    - このシステム自体をネストしたものにすることの検討
    - 「ネスト」だと部門横断的チームの妨げになると思うから、複数が作られてつながり合う形が良いと思うな
- > (8) Negative voting can provide a useful signal, but also has the potential to create polarization within group contexts (Weber, 2021). This has been observed empiri- cally within the context of quadratic funding rounds, such as those run by Gitcoin (Buterin, 2020). Running instances of plural management with and without negative voting could help further evaluate its psychological effects and impact on cooperative behavior.
- > (8) マイナス投票は有用なシグナルを提供する可能性がありますが、グループの文脈内で分極化を生み出す可能性もあります（ウェーバー、2021）。これは、Gitcoin（ブテリン、2020）によって実施された二次資金調達ラウンドの文脈で経験的に観察されています。マイナス投票のあるなしでプルーラル・マネジメントのインスタンスを実行することは、その心理的効果と協力的行動への影響をさらに評価するのに役立ちます。
    - マイナス投票はあるべきかどうか
    - 個人的にはあるべきだと思うが、それによってモチベーションに影響があるというのもわかる
    - 今回誰でも投票に参加できるようになったわけだがそれ以前からある問題だよね
        - プルリクする側の視点では自分のプルリクをリジェクトして欲しくない
        - プルリクを受ける側の視点では、もちろんプルリクをリジェクトする選択肢は必須
    - リジェクトされてもあなたの人間性を否定したわけではないんだよ、というメッセージが有効か？
- > (9) When the result of a prediction market can be influenced by the members participating in it, the possibility of collusion to manipulate outcomes arises (Ottaviani and Sørensen, 2007). An analysis of how participants in plu- ral management vote with and without the opportunity to predict outcomes would be useful for understanding what if any limitations should be placed on rewards from this activity.
- > (9) 予測市場の結果がそれに参加するメンバーによって影響を受ける場合、結果を操作するための共謀の可能性が生じます（オッタビアーニとソーレンセン、2007）。プルーラル・マネジメントの参加者が、予測の機会がある場合とない場合でどのように投票するかについての分析は、この活動からの報酬にどのような制限を設けるべきかを理解するのに役立ちます。
    - 予測市場を導入したのは今回の提案の新しいポイントだと思う
    - それが有効に機能するのかどうか、まだ実践的な実験によって検証はされてない
    - 多分Gov4gitに真っ先に実装される(著者の一人がGov4gitなので)

# 6 Conclusion
- > Plural management is a protocol for bridging between the desired properties of rigid management hierarchies and flat decentralized organizations, allowing for the dynamic al- location of management authority based on longitudinal contributions of individuals to outcomes and management decisions. Through the adjustment of a voting-prediction discount parameter, administrators can reward new or low credit-holding members of a community for their work in performing due diligence of new contributions in line with the expected standards or higher-authority mem- bers. This management approach, which uses quadratic funding to solicit preference from a broad base of partici- pants, creates a closed credit system with no external mon- etary value, that can only be exercised within the project. While this design of a management protocol raises open questions about implementation choices and net outcomes on organizations’ productivity, it can built using standard software design practices and fits naturally into the work- flow of open-source projects. In total, this model of plural management could present a dynamic scalable approach to distributing authority and rewarding participation across projects of any scope, mission, or size.
- > プルーラル・マネジメントは、厳格な管理階層とフラットな分散型組織の望ましい特性の間を埋めるためのプロトコルであり、個人の成果や管理決定への長期的な貢献に基づいて管理権限を動的に割り当てることを可能にします。投票予測割引パラメーターの調整を通じて、管理者は新しいメンバーや低クレジット所有のメンバーに、予想される基準や高権限メンバーに沿った新しい貢献の適切な調査を行う作業に対して報酬を与えることができます。この管理アプローチは、幅広い参加者からの好みを募るために二次資金調達を使用し、プロジェクト内でのみ行使可能な外部通貨価値のない閉じたクレジットシステムを作成します。この管理プロトコルの設計は、実装の選択と組織の生産性に対する全体的な成果に関する未解決の問題を提起しますが、標準的なソフトウェア設計の慣行を使用して構築することができ、オープンソースプロジェクトのワークフローに自然に適合します。合計すると、このプルーラル・マネジメントモデルは、どのような規模、使命、またはサイズのプロジェクトにおいても、権威を分散し、参加を報酬するための動的かつスケーラブルなアプローチを提示する可能性があります。

- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 慈悲深い独裁者に依存するか、善良なメンバーしかいないことに依存するか、、、
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 一般の政治でやるならゼロトラスト的な設計をしたい
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> システムが複雑になると理解できなくて取り残されたり反対して新しいシステムへの移行が厳しくなったりしそうで、未来人と村人の間がちぎれる話が起こりそう(一般的な感想です)
    - ちぎれるのが統治システムで起こるのはクリティカルに見える
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/> 温度感の見える化は有用そう。だけど、共通の数字として見えるわけではなさそう(人によって、テーマとそれに vote した人間の組に対してどのくらいの重みをつけるかは違う)。数字化するのは賛成だけど貨幣的なものでやるのは厳しいんじゃないかという気持ち。

時間が余ったらこれを見る
- 参考資料: [Gov4Git community dashboard · Issue #263 · pluralitybook/plurality](https://github.com/pluralitybook/plurality/issues/263)

