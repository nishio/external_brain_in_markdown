---
title: "ABC180E"
---

from [[ABC180]]
[E - Traveling Salesman among Aerial Cities](https://atcoder.jp/contests/abc180/tasks/abc180_e)
- ![image](https://gyazo.com/f3e649bb12de0bbd15495e3c67a3523e/thumb/1000)
- 考えたこと
    - 17の階乗は十分大きい
    - [[巡回セールスマン問題]]([[TSP]])を[[bitDP]]で解く問題
    - サンプル2に出てくる「同じ都市を2回通っても良い」が少し違うか？
        - でも直接移動しないで他の都市を経由した方が得になるパターンがない気がする
    - bitDPで巡回セールスマン問題を解いてる記事を適当にググって参考にする
        - [【競プロ】bitDP入門(緑・水コーダー向け) - Qiita](https://qiita.com/xryuseix/items/7ca1aec4b1a7e8bff997)
    - 「都市1からすべての都市を訪問するまで」ではなく「都市1に戻るまで」なので少し修正が必要
    - 修正して小さいサンプルは通るけど、大きいサンプルが通らない、原因を見つけられないままコンテスト終了
- コンテスト後
    - ACしてる人の実装を持ってきて、ランダム入力で食い違いが発生する小さいサンプルを作る
    - `5, [[1, 1, 0], [1, 2, 1], [1, 1, 1], [1, 2, 0], [2, 0, 1]]`が、本当は7なのに8と返してしまう
- [[蟻本]]を見たらループの場合のTSPのコードがあったので参考にしたらあっさり26分でACした
python

```
def solve(N, XYZS):
    import sys
    INF = sys.maxsize  # float("inf")

    dist = []
    for i in range(N):
        a, b, c = XYZS[i]
        ds = []
        dist.append(ds)
        for j in range(N):
            p, q, r = XYZS[j]
            ds.append(abs(p - a) + abs(q - b) + max(0, r - c))

    SIZE = 2 ** N
    memo = [[INF] * N for _i in range(SIZE)]
    memo[-1][0] = 0
    for subset in range(SIZE - 2, -1, -1):
        for v in range(N):
            for u in range(N):
                if (subset >> u) & 1 == 0:
                    mask = 1 << u
                    memo[subset][v] = min(
                        memo[subset][v],
                        memo[subset | mask][u] + dist[v][u]
                    )
    return memo[0][0]
```

- 考察
    - Qiitaの方はsubsetごとに最終頂点を配列lastの値で持ってる
    - 蟻本の方は添え字で持ってる
    - Qiitaの方は問題条件が「頂点0から始めて、全部の頂点を辿る最短のパス」なので、頂点0に戻る道が含まれてない
        - このアルゴリズムで最短のパスを見つけたとしても、そこからの帰り道が高コストかもしれない
    - 今回の問題と蟻本の例は最短の閉路
        - だからQiitaの解説とは根本的に問題条件が違う
    - 蟻本の側の解説
        - 頂点0からスタートするが、訪問済み頂点集合を考える上で頂点0は最初は含めない
        - こうすることで「訪問済み頂点集合が全集合になった」時「頂点0に戻ってきた」ことを意味するので、戻り道も含めた問題条件に適用できる
        - 逆順でDPしていることには何か深い意味があるのだろうか？
            - 正順でも問題なく動くから深い意味はなさそう
python

```
    memo[0][0] = 0
    for subset in range(1, SIZE):
        for v in range(N):
            for u in range(N):
                mask = 1 << u
                if subset & mask:
                    memo[subset][v] = min(
                        memo[subset][v],
                        memo[subset ^ mask][u] + dist[u][v])
    return memo[-1][0]
```


