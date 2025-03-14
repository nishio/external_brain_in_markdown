---
title: "全方位木DP"
---

全頂点を根として[[木DP]]をする場合、有向辺を定義域とすれば結果の使い回しができてO(N)になるというテクニック
![image](https://gyazo.com/5f02c5706cebeceb42cc0f5e7ed2843f/thumb/1000)
- 通常の木DPは特定の根について辺の本数をNとしてO(N)
    - 木なので辺は頂点-1本
- すべての頂点について木DPをしたい時、単純に繰り返すとN^2のオーダーになる
    - 最初の木DPの時の結果を再利用すると2Nステップになる
- 図では「Aを通る最長パスを求めよ」をまず7ステップの木DPで求めている
    - ある特定の根から子供の木の深さを調べて、その大きい方から二つを足したものがその頂点を通る最長パス
    - 次に「Bを通る最長パスを求めよ」を解く際に、Aについての木DPの結果を再利用して1ステップで完了している
- この再利用が容易な形で計算結果を持つには頂点ではなく有向辺が定義域である必要がある
    - Aが親である時のEとFが親である時のEは別物なので
    - ![image](https://gyazo.com/7b2da7c244be0051fd9755847b7e7d22/thumb/1000)
    - 逆の言い方をすると、単独の木DPの時は「有向辺の根本」と「根以外の頂点」が一対一対応するので頂点を定義域にできているだけ
    - 有向辺を文字通り「始点と終点のタプル」で持っても動くのだけど、辺を「根に近づく勉強」「根から遠ざかる辺」の2つに分けるとそれぞれ始点と終点が根以外の頂点と一対一対応するので楽
        - 見かけた実装では最初に無向グラフを頂点から幅優先探索して「根に近づく辺」を取り除いてた
        - 探索順を保管することで、再帰呼び出しなく実装できる
        - 最初の木DPは幅優先の逆順で処理できる、次のフェーズで正順で処理して完了
- 集計に工夫が必要
    - ある頂点に辺が1万本つながっている(位数1万)とする、この頂点から出る有向辺の値は残りの9999本から求められる
    - この集計処理が位数のオーダーだと位数をNとしてO(N^2)のオーダー
        - 一つの頂点に辺が集中しているグラフの時に大変なことになる
        - 素朴に「木」と言った時に多くの人の脳内に浮かぶのは位数が小さいグラフ
        - 問題条件で明示的に除外していない以上テストケースはこのパターンを突いてくる
    - この集計をO(1)にするテクニックは全方位木DPとは無関係
        - 集計処理の性質に依存する
        - 「N個の数から一つを取り除いたものの和を取りたい」
            - 総和を求めておいて、一つ引く
            - 一般化すると「[[逆元]]が存在する二項演算」ならこれが使える
        - 「N個の数から一つを取り除いたものの積を取りたい」
            - 乗算は逆元がない(0で割れない)
            - [[単位元]]があって[[結合則]]が成り立つなら[[左右から累積積]]できる
            - 剰余がついててもこのクラスになる
- 根に集まる計算をした後、根から順に上記の「子に降りる矢印をO(N)で計算」する
    - ![image](https://gyazo.com/9cdfd1567858c3214c5f7147643700fe/thumb/1000)
    - 図ではAの子に対して一括で計算している
    - そうすると子B,D,Eはそこに集まる矢印が全部確定したので最終結果を出すのに必要な情報が揃う
    - これを繰り返していくことで幅優先探索の順で答えが確定していく

参考
- [木DPと全方位木DPを基礎から抽象化まで解説【競技プログラミング】 | アルゴリズムロジック](https://algo-logic.info/tree-dp/)
- [†全方位木DP†について - ei1333の日記](https://ei1333.hateblo.jp/entry/2017/04/10/224413)
- [F - Distributing Integers](https://atcoder.jp/contests/abc160/tasks/abc160_f)
- [https://maspypy.com/atcoder-参加感想-2019-03-28abc-160](https://maspypy.com/atcoder-参加感想-2019-03-28abc-160)

[[動的計画法]]