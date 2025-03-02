
集合の併合と、共通の集合かどうかのチェックが高速な[[データ構造]]。
グラフに辺を追加して、二頂点が連結かどうかのチェックが高速、という捉え方もできる。

N個の対象間の関係に関して、それがiffに分解できるならグラフの辺として記述できる
- 例えばグーチョキパーのいずれかである対象があったときに「xはyに勝つ」は、「xがグーである iff yがチョキである」のような3つのiffに分解できるので3Nの頂点集合に3本の辺を追加することに相当する
- 連結成分は条件を充足する解に相当する
- iffでない場合→[[2-SAT]]

[https://judge.yosupo.jp/submission/12685](https://judge.yosupo.jp/submission/12685)

- [[素集合データ構造]] [Wikipedia](https://ja.wikipedia.org/wiki/%E7%B4%A0%E9%9B%86%E5%90%88%E3%83%87%E3%83%BC%E3%82%BF%E6%A7%8B%E9%80%A0)
- [[Disjoint Set Union]] ([[DSU]])
- [[Union-Find]]
