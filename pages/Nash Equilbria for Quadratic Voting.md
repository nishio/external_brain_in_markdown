---
title: "Nash Equilbria for Quadratic Voting"
---

from [[Quadratic VotingとPlural Management勉強会]]
Nash Equilbria for Quadratic Voting
[Nash Equilbria for Quadratic Voting](https://arxiv.org/abs/1409.0264)
2014
(概要の訳) 二元的な決定を下す有権者が、中央集権型のクリアリングハウスから票を購入し、購入した票数の二乗に相当する代金を支払います。効用がuでv票を購入したエージェントの純利益は、$Ψ(S_{n+1})u−v^2$となります。ここで、Ψは-1から+1の間の値を取る単調関数であり、$S_{n+1}$は選挙に参加するn+1人の有権者が購入した全投票の合計です。有権者の効用は、コンパクトなサポートを持つ確率分布$F_U$からのランダムサンプリングによって生じるとします。各有権者は自身の効用を知っていますが、他の有権者の効用は知らず、ただしサンプリング分布$F_U$は知っています。このゲームのナッシュ均衡が記述されています。これらの結果から、任意のナッシュ均衡の期待される非効率性は1/nのように減少することが示唆されます。

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>[[コンパクトなサポート]]とは、数学において、ある関数が有限の区間でのみ非ゼロの値を取り、それ以外の範囲ではゼロになる性質を持つことを指します。
- 最初の1票が100円の時に、100億円払って10000票投じてくる人はいないよね、という仮定<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>流れを簡単に解説して
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>この論文は、二項選択の[[集合的意思決定問題]]における [[quadratic voting]] (QV) メカニズムの効率性を理論的に分析したものです。
論文の主な流れは以下の通りです。

- QVメカニズムのモデル設定を説明。各投票者は自分の選好の強さに基づいて票を購入し、合計票数で決定が下される。
- Nash平衡の存在を示し、平衡における投票者の行動の基本的性質を論じる。
- 投票者母集団の平均選好が0の場合、十分に大きな母集団サイズのもとでは、平衡での非効率性が0に収束することを示す。
- 投票者母集団の平均選好が0でない場合、平衡での投票総数が一定値に集中し、非効率性が0に収束することを示す。ただし平衡では不連続点が生じうる。
- 平衡解析のために、独立同分布の確率変数の和に関する確率不等式や中心極限定理の精緻な応用を行う。
- シミュレーションによる数値例は示さず、理論的な漸近的効率性の証明に焦点を当てている。

以上のように、この論文はQVメカニズムについて、大母集団のもとでの Nash平衡の性質を理論的に分析し、その漸近的効率性を証明したものだと言えます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Nash平衡の存在はなぜ言える？
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>この論文では、以下の2つの理由からNash平衡の存在が言えると主張しています。

### 1. Reny (2011) の定理4.5を適用できる
Reny (2011) は、ベイジアンゲームにおけるNash平衡の存在定理を示しています。この定理の条件を本論文のQVモデルが満たすことを確認することで、Nash平衡の存在が保証されます。

具体的には、以下の条件を満たすことを確認しています。
- 各投票者のタイプ（選好の強さ）に条件付けた期待利得が連続である
- タイプに応じたベストレスポンスが単調であり、supermodularityを満たす

### 2. 最適反応対応の単調性
投票者の最適反応対応（どのタイプがどれだけ投票するか）が、タイプに関して単調増加であることを示しています。これは、選好が強い（タイプの値が大きい）投票者ほど多くの票を購入することを意味します。

この単調性は、投票者の期待利得がタイプと購入票数に関してsupermodularであることから導かれます。

以上の2点から、本論文で扱うQVモデルにおいてNash平衡が存在することが示されています。ただし、平衡の一意性は一般には成立しないことにも言及されています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>投票者母集団の平均選好とは？
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>本論文では、各投票者の選好の強さを表すタイプ (type) が実数値 u で表現され、これが確率分布関数 F に従って分布していると仮定しています。平均選好 μ は、この確率分布のもとでのタイプの期待値として定義されます。

`μ = E[u] = ∫ u dF(u)`

ここで、μ > 0 の場合は投票者集団が全体として選択肢 +1 を選好する傾向が強く、μ < 0 の場合は選択肢 -1 を選好する傾向が強いことを意味します。μ = 0 の場合は、投票者集団としては両選択肢に対して中立的であることを表します。

本論文の主要結果の1つは、平均選好 μ の値に応じてNash平衡の性質が大きく異なるというものです。特に、μ = 0 の場合とμ ≠ 0 の場合で、平衡の連続性や漸近的効率性の結果が質的に変化することが示されています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>平衡での非効率性とは？
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>平衡での非効率性とは、QVメカニズムのもとでのNash平衡において、集合的意思決定の結果が投票者全体の効用の総和を最大化していない程度を表します。本論文では、非効率性の指標として expected inefficiency (EI) を定義しています。
(...数式省略<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>)EI は、実現された集合的意思決定のもとでの投票者全体の効用を、最大可能な効用の2倍で基準化し、1/2 からの差を取ったものです。
EI = 0 のとき、QVメカニズムのもとでの平衡が完全に効率的であること（投票者全体の効用を最大化していること）を意味します。一方、EI > 0 のとき、非効率性が存在することを表します。

本論文の主要結果は、十分に大きな投票者母集団のもとでは、EI が投票者数 N → ∞ のとき 0 に収束するというものです。つまり、QVメカニズムは漸近的に効率的であることが示されています。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
> 投票者母集団の平均選好が0でない場合、平衡での投票総数が一定値に集中し、非効率性が0に収束することを示す。
どのような理由で？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
投票者母集団の平均選好 μ が0でない場合、平衡での投票総数が一定値に集中し、非効率性が0に収束することが示されています。これは以下のような理由によります。

### 投票総数の集中
十分に大きな投票者母集団のもとでは、平衡での投票総数 V が一定値 ξ に確率収束することが示されています。(...数式省略<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>)
直感的には、この集中は、選好が強い投票者（extremists）が戦略的に投票を控えるためです。もし extremists が大量の票を投じれば、投票総数が大きく変動してしまいます。そこで、extremists は投票を控え、投票総数を一定の範囲内に抑えるインセンティブが働くのです。

### 非効率性の収束
投票総数が ξ に集中することから、集合的意思決定の結果 Ψ(V) が確率1で Ψ(ξ) に収束することが示されます。
また、十分に大きな母集団のもとでは、投票者全体の選好の総和 U が μN に近づくことから、
`E[UΨ(V)] ≈ μN Ψ(ξ) ≈ 2E[|U|]`
が成り立ちます。これは非効率性の指標 EI が0に収束することを意味します。

以上のように、平均選好 μ ≠ 0 のとき、extremists の戦略的行動により投票総数が一定値に抑えられ、結果として集合的意思決定が効率的になることが示されているのです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
> 直感的には、この集中は、選好が強い投票者（extremists）が戦略的に投票を控えるためです。もし extremists が大量の票を投じれば、投票総数が大きく変動してしまいます。そこで、extremists は投票を控え、投票総数を一定の範囲内に抑えるインセンティブが働くのです。
ここがわからない

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>...
もしextremistsが大量の票を購入すれば、投票総数Vが大きく変動してしまいます。これは、集合的意思決定のルールΨ(V)が不連続に変化することを意味します。

例えば、投票総数が正から負に変われば、Ψ(V)は+1から-1へと不連続にジャンプします。このとき、extremistsは自分の選好する選択肢が実現しない可能性が高まってしまいます。

そこで、extremistsは「他のextremistsが大量の票を購入するだろう」と予想し、自分の投票数を控えめにするインセンティブが働きます。つまり、extremists同士で投票数を抑制し合う戦略的行動が生まれるのです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
> もしextremistsが大量の票を購入すれば、投票総数Vが大きく変動してしまいます。これは、集合的意思決定のルールΨ(V)が不連続に変化することを意味します。
ここがわからない

<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>....

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>自分の好む結論が出ないことが予想されるextremistsはたくさん票を買うのでは？

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>その通りですね。自分の好む結論が出ないと予想されるextremistsが、たくさん票を買おうとするインセンティブがあることは、ご指摘の通りです。

実際、本論文のモデルでは、平均選好μが0でない場合、extremistsが大量の票を購入することで不連続点が生じうることが示されています（Theorem 3）。

具体的には、十分に大きな投票者母集団のもとでは、ほとんどすべての投票者が「moderate（穏健派）」となり、投票総数をξ付近に収めるように振る舞います。しかし、extremistsは確率0ではあるものの、必ず存在します。

このextremistsは、投票総数をξから大きくずらすために、大量の票を購入しようとします。その結果、投票総数Vが不連続に変化し、集合的意思決定が覆される可能性が生じるのです。

ただし、このようなextremistsの出現確率は、投票者数Nが大きくなるにつれて指数的に減少することが示されています。つまり、十分に大きなNのもとでは、extremistsの影響は無視できるほど小さくなります。

そのため、全体としては、投票総数がξ付近に集中し、集合的意思決定が効率的になる、というのが本論文の主要な結論なのです。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>"extremistsの出現確率は、投票者数Nが大きくなるにつれて指数的に減少する" はどの式で示されてますか
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
extremistsの出現確率が投票者数Nが大きくなるにつれて指数的に減少することは、Theorem 3の証明の中で示されています。
具体的には、証明の中で、extremistsの数Neが以下の確率不等式を満たすことが示されています（式(57)）。
P{Ne ≥ k} ≤ (α^k / k!) · (1/n^(k/2)) for all k ≥ 1
ここで、αは選好分布に依存する定数です。
この不等式は、Neがkより大きくなる確率が、Nが大きくなるにつれて指数的に減少することを意味しています。

論文を見る(p.32)<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
![image](https://gyazo.com/fef84a9d9b3306bfddcad3d1f35a28e1/thumb/1000)

<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>(続き)
特に、k=1の場合を考えると、
P{Ne ≥ 1} ≤ α / √n
となります。つまり、extremistsが1人以上存在する確率は、O(1/√n)のオーダーで減少するのです。

なるほどな〜<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 「直感的には〜」と説明された直感的な説明が僕には直感的に正しいと判定できなかったので問い詰めたが、大量に投票するようなプレイヤーが0人に収束するのであれば納得
- これはQVに対する典型的な反発「金持ちがたくさん票を買うのでは？」に対する反論にもなっているな
