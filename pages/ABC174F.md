---
title: "ABC174F"
---

[F - Range Set Query](https://atcoder.jp/contests/abc174/tasks/abc174_f)
![image](https://gyazo.com/d1e4ee6d9ee7b595405a406cf1c6fbe7/thumb/1000)

- 考えたこと
    - 範囲内に色ciが存在するかどうかを対数オーダーで判定できれば間に合う
    - 二分探索
- 実装
    - 7分で実装、提出、TLE
    - あ、全然ダメだ、各色ごとN件につき対数オーダーで範囲内にあるかどうか判定できてもO(QNlogN)だ
- 改めて考察
    - [[クエリの先読み]]して[[二次元の片方を時間軸にする]]か
        - それでも最悪O(QN)か
    - 玉の色の集合を2^nのブロックごとに作る
        - 集合は全部で2N-1個
        - logN回のマージで要求された区間の色の集合ができる
            - しかし普通にやるとマージが重くて結局O(QN)
            - マージが軽い[[二項ヒープ]]を使う？
- 公式解説
    - 区間クエリといえばセグメント木だが、マージが重い
    - [[クエリの先読み]]して[[二次元の片方を時間軸にする]]
        - 各時点での各色の「最も右の球の場所」をメンテする
        - これがLより大きければ、範囲内にその色がある、定数オーダー
        - しかしこれでもO(QN)
        - 各色の「最も右の球の場所」を[[フェニック木]]に入れる
            - 個数を数えることが範囲和で対数オーダー
            - なるほど、ここがポイントか
            - [[多くのものと大小比較→フェニック木]]

- 3TLE

[[クエリがたくさん問題]]
from [[ABC174]]
ARC174F
- [https://hama-du-competitive.hatenablog.com/entry/2016/10/01/001418](https://hama-du-competitive.hatenablog.com/entry/2016/10/01/001418)
- [https://twitter.com/maspy_stars/status/1290139299011129344?s=21](https://twitter.com/maspy_stars/status/1290139299011129344?s=21)
- [https://twitter.com/tktk_snsn/status/1290222202843889665?s=21](https://twitter.com/tktk_snsn/status/1290222202843889665?s=21)
- [[Mo's algorithm]]
