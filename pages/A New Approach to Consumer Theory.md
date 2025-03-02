
[[Lancaster1966]]
[[Lancaster]]
A New Approach to Consumer Theory
Author(s): Kelvin J. Lancaster
Source: The Journal of Political Economy, Vol. 74, No. 2 (Apr., 1966), pp. 132-157 Published by: The University of Chicago Press
Stable URL: [http://www.jstor.org/stable/1828835](http://www.jstor.org/stable/1828835)
Accessed: 22/09/2008 02:58


従来の消費者モデルでは、財(good)の間の関係が、同じ財か違う財かの二択だった
- バターとマーガリンの関係と、靴と船の関係は同じ
- 赤のシボレーとグレーのシボレーは同じ財なのか違う財なのか？

そこで効用が財ではなく特徴に対して定義されるモデルを作った

- 以下の3つの要素で新しいモデルを作る(p.134)
    - 1: 効用(utility)は特徴(characteristic)の関数(従来は財の関数だった)
    - 2: 財は1つ以上の特徴をもち、特徴は複数の財で共有される
    - 3: 財の組み合わせがもつ特徴は、個別の財のもつ特徴とは異なっている
![image](https://gyazo.com/d02de0d3d274b728849fd3502ecdf4db/thumb/1000)
これによって、例えば赤のシボレーとグレーのシボレーは「大部分の特徴が共通で、色の特徴だけ異なっている財」という表現ができるようになる。

### 数式でのモデル表現
後で説明するSimplified modelではActivity(購入などの行為)とGoodが1対1対応するが、一般のモデルではそうではないのでGoodをx, Activityをyで表現する。
$x_j = \sum_k a_{jk} y_k$
$x = Ay$
ActivityとGoodが1対1対応する時には、Aが単位行列で $x = y$ となる。
このActivityとGoodの関係を表現するAは、linear(線形)でobjective(客観的)と仮定されている。

Activity yとCharacteristic zの関係も同様に線形で客観的と仮定する。
$z_i = \sum_k b_{ik} y_k$
$z = By$

効用Uはzの関数である。従来モデルではxの関数であったのと対照的。
- 効用Uは線形とは限らない([[限界効用逓減の法則]])

linear budget constraint(線形予算制約)を price vector p を用いて $px \leq k$ と表現する。
- (k のことを、単なる添字風に使ったり、大小関係が意味を持つ値として使っていたりして混乱の元であるが、複数の財の組み合わせを考えない場合単なる「価格と財の内積が一定値以下」という制約と考えて良い。Lancasterは後の議論のために k を level of activity として使おうとしたのだ)

まとめると
$\text{Maximize} U(z)$
$\text{subject to} px \leq k$
$\text{with} z=By,\quad x=Ay,\quad x,y,z \geq 0$
となる

ActivityとGoodがone to one対応するSimplified Modelでは、xとyが同一視されるので
$\text{Maximize} U(z)$
$\text{subject to} px \leq k$
$\text{with} z=Bx,\quad x,z \geq 0$
となる

従来のモデルでは効用がGood-space([[G-space]], 財の空間)で定義されていたので、予算制約との関係はIndifference-curve([[無差別曲線]])で表現できていたが、このモデルでは効用がCharacteristic-space([[C-space]], 特徴の空間)で定義されるので、写像が必要。
- p137
    - a) G-space上でのconvex set(凸包)はC-space上でも凸包なので、予算制約線はC-spaceでも凸包
    - b) Bに逆行列があるとは限らないので、C-space上の任意のzが対応するG-space上のxを持つとは限らない
    - c) もし逆行列があるなら、これも凸包を凸包に写す写像になるので、Uのconvexityは保存される

### the structure of consumption technology
Simplified modelだとAは消えてしまうので、Bが重要。このBをconsumption technology([[消費技術]])と呼ぶ。このBの形状によって3パターンに分けて議論が行われる。
- 1: 特徴の数が財の数と同じである場合
    - いくつか条件をつけると従来モデルに帰着する
- 2: 特徴の数が財の数より多い場合
    - Bx=zは連立方程式として捉えると、「変数の個数以上の等式がある」ので一般に解を持たない
    - だからスライス(多すぎる特徴の一部を無視すること)して考える
    - この時にconvexityが保たれることをLancasterは重視している
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>にとっては「given zに対応するxの厳密解が存在しないことに現実社会に何の意味が？」と感じる。現実の消費者は「自分の得たい特徴z」が市場に出回っている商品で充足されない場合に、類似の商品で十分満足できるならそれを買うわけなので、効用最大化のフレームワークに吸収される。厳密解の必要はない。
- 3: 財の数が特徴の数より多い場合
    - この時、Bx=zを満たすxは複数存在する
    - そこで顧客はその複数のxの中から選択をする。
        - その選択のefficiencyはminimum costである(効率的市場仮説の意味での「効率的」が使われている)
    - given z*に対して効率的なx*を求める最適化は
        - $\text{Minimize} px$
        - $\text{subject to} Bx=z^*, x\geq 0$
    - z*を動かした時に、px=kが満たされるzの集合をcharacteristic frontierと呼ぶ
        - これはgivenな予算制約の中で最大限得られる特徴の集合の境界を示す

ここまででモデルの説明は終わりで、後は色々な問題にこのモデルを当てはめていく

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>の感想
- 1966年時点の計算機リソースを考えると仕方ないことではあるが財の空間が有限である
    - 新製品開発などの文脈を扱う上では「作りうる無数の商品の中から、顧客の効用が高そうなものを選ぶ」という行動が自然に行われるので、財は無数にある
    - G-spaceを数学的に「無限次元の空間」として扱うか(これは突飛なことではなく、近年の自然言語処理では単語の空間を無限次元と捉えて[[ディリクレ過程]]などで事前分布を入れたりする)
    - もしくは十分に大きな次元の空間で近似するか
- 線形問題として取り扱っている
    - 解析的に解けなくなるから仕方ないのだろうと思うが、財の量は連続値なので、限られた予算で「3.5インチHDDを1/3個と5インチHDDを2/5個買う」という行動が可能になってしまう
    - 現実的にはカメラを半分買うとかはあり得なくて、量り売りしている布や水や穀物などでのみ近似的に成り立つ
    - これはそもそも財の選択xをベクトルとして扱っているせい
    - 「顧客は財を1つだけ買う」というone-hot制約を入れると、C-space上の1点がG-space上の1点に対応するようになる
        - 代わりに財のcombinationは扱えなくなるが、得手不得手の明確な方が良い
    - G-spaceが粉砕されることによって予算制約線の議論は困難になるが、[[Adner 2002]]がやっているように 価格の逆数を特徴の1つとして加えれば良い
        - 代わりにC-space上での技術制約線の議論が重みを増す
