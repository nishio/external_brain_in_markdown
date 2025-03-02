
長さNの静的な値の列が与えられた時に、前処理O(NlogN)で、その列の上の区間に対する演算がO(1)で計算できるようになるデータ構造

使える演算は具体的にはminなど、argminもOK
- [[交叉半束]]
    - [[結合法則]]: $(a * b) * c = a * (b * c)$
    - [[交換法則]]: $a * b = b * a$
    - [[冪等性]]: $a * a = a$

構築O(N log N)
- 各点から2ベキの長さの区間のminを計算
- 2^kの長さの区間は半分の長さの区間2つから定数オーダーで計算可能なので小さい方からDPする

クエリー
- クエリー区間の長さより小さい最大の長さの計算済み区間を2つ使ってクエリ区間を覆う
- 例えば1〜7の区間に対して1〜4と4〜7で覆う
- クエリ区間の最小値は2つのどちらかの区間での最小値

列が更新される時は[[セグメント木]]を使う
- [[スパーステーブルとセグメント木]]

木の[[最小共通祖先]]を[[オイラーツアー]]+[[Range Minimum Query]]で求める場合に。
- [最小共通祖先 [いかたこのたこつぼ]](https://ikatakos.com/pot/programming_algorithm/graph_theory/lowest_common_ancestor)

[スパーステーブル(Sparse-Table) | Luzhiled’s memo](https://ei1333.github.io/luzhiled/snippets/structure/sparse-table.html)

2次元に拡張できる
- [競技プログラミングにおけるSparse Table問題まとめ - はまやんはまやんはまやん](https://www.hamayanhamayan.com/entry/2018/01/03/035508)
- [[2D Sparse Table]]
    - [[2D Range Minimum Query]]
        - [2D Range Minimum Query in O(1) - Codeforces](http://codeforces.com/blog/entry/45485)

[[スパーステーブル]]
