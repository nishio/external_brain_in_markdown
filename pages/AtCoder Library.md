
> 様々なアルゴリズムを [[AtCoder]] 側で実装した
- [https://atcoder.jp/posts/517](https://atcoder.jp/posts/517)

[[AtCoder Library Practice Contest]]
- 練習用コンテストで一通りACした解説

とりあえず確認してみたら1/3から1/2くらい既に実装してあった。今はリポジトリにバラバラに散らばってるので後でACLと同じディレクトリ構造にしてMITライセンスにしとこう。
残りの未実装なものは公式が「これは頻出アルゴリズムだ」と言ってるわけだからなるはやで実装する。

> AtCoder Library の Python 実装，普通にいろんなアルゴリズムを実装するとかはすでにいっぱいある（≒ yosupo judge や AOJ から取ってこればよい）はずだから，numpy/scipy/networkx とか cython とかでゴリゴリに高速化したものができてほしい [src](https://twitter.com/n_knuu6/status/1303026130279047168)
- Practice ContestのAll Submitの所要時間順ランキングがライブラリ速度を競い合う場になるのではないかと思ってる
- 僕は以前[[Numba]]や[[Cython]]での高速化にハマってたのだけど、最近は一周回ってPyPyで柔軟性を犠牲にせずに速くすることに興味がある

内容
- [[フェニック木]]
    - 部分和の計算と要素の更新の両方を効率的に行える木構造(Binary Indexed Treeとも呼ばれる)
    - [B: 600ms](https://atcoder.jp/contests/practice2/submissions/16567562) PyPy暫定一位
- [[セグメント木]] [J - Segment Tree](https://atcoder.jp/contests/practice2/tasks/practice2_j) [454 ms](https://atcoder.jp/contests/practice2/submissions/16567936)PyPy暫定一位  [K - Range Affine Range Sum](https://atcoder.jp/contests/practice2/tasks/practice2_k)
    - 固定個数の要素がランダムアクセスで更新される時に総和や最小値をO(logN)で求めることができる木
- [[遅延伝搬セグメント木]] [L - Lazy Segment Tree](https://atcoder.jp/contests/practice2/tasks/practice2_l)
- 文字列アルゴリズム詰め合わせ
    - [[接尾辞配列]]
    - [[LCP array]] [I - Number of Substrings](https://atcoder.jp/contests/practice2/tasks/practice2_i)
        - [752ms](https://atcoder.jp/contests/practice2/submissions/16567345) PyPy暫定一位
    - z_algorithm
- 数学アルゴリズム詰め合わせ
    - pow_mod
    - inv_mod
        - [[Pythonでの累乗・逆数・階乗・階乗逆数・組み合わせ]]で実装した
    - crt
        - [[中国剰余定理]]
    - [[floor_sum]]
        - [C - Floor Sum](https://atcoder.jp/contests/practice2/tasks/practice2_c)
- 畳み込み [F - Convolution](https://atcoder.jp/contests/practice2/tasks/practice2_f)
    - Pythonだと[[np.convolve]]とかに相当するやつ
    - [[Two Snuke]]ではint64に収まらなくて自前でやった
- Modint 自動でmodを取る構造体
    - Pythonだと演算子のオーバーロードで実現したら見た目は綺麗だけど、これを使うシチュエーションは関数呼び出しのオーバーヘッドを払えない状況だと思う
    - [[長整数が速い]]を使った攻略が良さそう
- グラフ
    - [[DSU]]
        - 無向グラフに対して、辺の追加、頂点が連結かの判定、をならし O(α(n)) 時間で処理
        - [[UnionFind]]ってこと？
        - [A: 277ms](https://atcoder.jp/contests/practice2/submissions/16567503) PyPy暫定一位
    - Maxflow [[最大流]] [D - Maxflow](https://atcoder.jp/contests/practice2/tasks/practice2_d)
    - MinCostFlow [[最小費用流]] [E - MinCostFlow](https://atcoder.jp/contests/practice2/tasks/practice2_e)
    - [[SCC]] [G - SCC](https://atcoder.jp/contests/practice2/tasks/practice2_g)
        - 有向グラフを強連結成分分解
    - [[2-SAT]] [H - Two SAT](https://atcoder.jp/contests/practice2/tasks/practice2_h)
        - $\bigvee (x_{i0} = v_{i0} \wedge x_{i1} = v_{i1})$の形の論理式を充足する割当が存在するかを判定し、する場合にはその割当の一つを得る

ここで練習できる
- [https://atcoder.jp/contests/practice2](https://atcoder.jp/contests/practice2)
Python関連記事
- [AtCoder Library Practice Contest 参戦記 (Python) - Qiita](https://qiita.com/c-yan/items/46845ba9deea43930544)
