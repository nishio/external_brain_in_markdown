---
title: "ACL1A"
---

![image](https://gyazo.com/419c5eed2447e1c5b17564f460169cba/thumb/1000)
from [[ACL1]]
ACL1A
[A - Reachable Towns](https://atcoder.jp/contests/acl1/tasks/acl1_a)
- ![image](https://gyazo.com/5112bbd589d700784b75fee59ac15f73/thumb/1000)
- 考えたこと
    - [[SCC]]？いや関係が対称だから[[DSU]]か
    - Nが20万もあるので、辺の有無を明示的に取り扱う方法はNG
    - なんらかの順でDPできるのでは？
        - あらかじめソートしておく
        - 先頭(argmin x)を一つ取る
        - yの比較でグループが決まる
        - 残りから先頭を一つとる
        - 同じことの繰り返し
        - 既にグループになったものは無視できる？→できない
        - こういうパターンで、後からグループに参加する頂点がある
            - ![image](https://gyazo.com/bdcecf2ff9b7ed58a925acd41bb619d9/thumb/1000)

        - →これでは比較回数が二乗のオーダーだからダメ
    - グループの代表点が一つに決まるか？→決まらない
        - 注: これが勘違い
    - クイックソート的に真ん中あたりの値で分割したらlogNになったりするか？→ほとんど全ての点がバラバラのグループである場合にNG
    - 打つ手が思いつかない
- 勘違いの発生プロセス
    - 後から参加する頂点がグループのどの頂点につながるか予見不能だと考えた(勘違い)
    - ![image](https://gyazo.com/c156550389503f072d7ef77e868a4f60/thumb/1000)
    - 「頂点がxの小さい順に確認される」という条件がセットになることで、予見可能になる
    - 上の図の下側のパターンは出現しない
        - 新しい頂点(xi, yi)はグループの中のxが最小である頂点(x0, y0)より右にある ($x_i > x_0$)
            - まだ訪問されてない頂点だけかなるグループは存在しないから
    - xの小さい順に訪問することで下記が言えるようになる
        - yi < y0である
            - もしそうでないならx0<xi and y0<yiで既にグループに入っているはずだから
            - つまりグループのすべての頂点に対してyの条件は満たしている
        - もしこの頂点がグループに入るならグループ内のある頂点(xj, yj)に対してxi < xjである
        - この条件を判定するためにはグループの中でxの最も大きい頂点だけに注目すれば良い
        - →グループを一つの頂点で代表できるようになる
    - [[順番を固定することで覚えるべき情報を減らす]]が肝
- 続き
    - 公式解説満点解
        - > この操作の過程において、各連結成分のうち最も y座標が小さいものだけ残しておけば良いことがわかります、なのでこれをsetやstackなどで管理することにより、mergeの回数をならしでO(N) 回へ減らせます。
    - maspyさん
        - > 辺をたくさん張るとその分、今後見るべき頂点が減るため、辺を張る操作は償却O(N)回しか行われず、あとはこれを適切に実装すれば解けます。
    - 未使用の点を入れておく構造を考える。
        - Pythonのリストだと要素の削除は遅いから[[ゼロフィルのリンクトリスト]]かな…？
    - →「stackやsetを使って適切に実装すれば良い」の「適切」がよくわからない。
        - どんな実装でもすべての点が右肩下がりに並んでて連結でない時に各点で「自分よりyの大きいものがいるか？」をN^2/2回ぐらい比較するのでダメな気がする…
    - [submissions:maspy](https://atcoder.jp/contests/acl1/submissions/16920107)解読
        - あれ、このコード、大小比較をしてないぞ？
        - XとYが一対一対応なのを利用し、xからyへの写像とyからxへの写像に変換
        - [[フェニック木]]を使ってる
        - 定義域を町のY座標にし、未使用のところに1を立てる
        - y0よりも大きなyを持つ町を探したい場合
            - まずy0までのsumを計算しkとする
            - 「sumがk+1以上になる最初のy」を二分探索すれば「次に大きなy」が見つかる
            - どちらもlog Nオーダー
            - yが見つかればyからxへの写像もできる
        - まとめた: [[削除可能集合で不等号条件]]

- 公式解説O(N)解
    - 実は正方形の集まりで表現できる
    - [[二者間の関係からより大きな構造ができる]]の例
    - 連結成分はX軸上で隙間なく並んでいる
        - ![image](https://gyazo.com/419c5eed2447e1c5b17564f460169cba/thumb/1000)
        - 仮に隙間があるとする
        - 連結成分であることから2つのグループをつなぐ辺があり、その両端の点はyi<yj
        - 隙間にある点について
            - y<yjなら右のグループにつながってしまう
            - yi<yなら左のグループにつながってしまう
            - よってどちらのグループともつながらないことは不可能
            - これはそこが隙間であることに矛盾する
    - 対称性からyについても同様
    - よって以下のことが言える
        - ![image](https://gyazo.com/9558ab1f2a6d698b120754a1a85033ef/thumb/1000)
        - 未決定頂点で最もxが小さいp0を見る
        - p0より上にk個の頂点がありえるなら、これらは確実にp0と連結する
        - 1: k番目の頂点が見つかった時点で、少なくともそこまでは連結であることが確定する
        - 2: この時、そこまでのすべての頂点が正方形の領域に入っているなら、それ以降にこの正方形の中の頂点と連結する頂点はない
            - 今後出てくる頂点は他のどの頂点よりも低いから
            - そうでないなら正方形を広げていく
            - y軸の隙間の個数は必ず今後連結するから
    - AC
python

```
def solve(N, XS, YS):
    size = [0] * N
    x2y = [0] * N
    x2i = [0] * N
    for i in range(N):
        x2y[XS[i]] = YS[i]
        x2i[XS[i]] = i

    ymax = N - 1
    x = 0
    while x < N:
        start = x
        y0 = x2y[x]
        k = ymax - y0
        ymin = y0
        while k or ymax - ymin > x - start:
            x += 1
            y = x2y[x]
            if y0 < y:
                k -= 1
            ymin = min(ymin, y)
        end = x + 1
        s = end - start
        for x in range(start, end):
            size[x2i[x]] = s

        x += 1
        ymax = ymin - 1

    return size
```

