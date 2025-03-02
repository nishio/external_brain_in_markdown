---
title: "区間DP"
---

区間$[l, r)$を定義域とする動的計画法
![image](https://gyazo.com/c26ccf2850d1bbdee5d71cea1c3bc249/thumb/1000)
- どう求めるかに何パターンかある(組み合わせて使うこともある)
- 1: [[縮める区間DP]]
    - f(l, r)をf(l + 1, r)とf(l, r - 1)から求める
- 2: [[中割りする区間DP]]
    - f(l, r)をf(l, i)とf(i, r)から求める (l < i < r)
    - O(N^3)になる
        - 間に合わない時
        - フェニック木などで範囲和を高速化する
- 3: 列から条件を満たす列を取り除く回数
    - 図は[[PAST5L]]のもの
        - 条件を満たす3つの要素の並びを取り除くことができる
        - 取り除く個数の最大化をしたい
        - 1と2はやった上でそれに加えて3をやる
        - 線で表現された区間が取り除かれた後、残った丸が条件を満たすパターン

- [[DP L]]
- [[DP N]]
- [[ARC108E]]
- [[区間の削除]]　[[区間の除去]]
    - [[PAST5L]]
    - [https://algo-logic.info/range-dp/](https://algo-logic.info/range-dp/)
- [[回文]]


[https://www.hamayanhamayan.com/entry/2017/02/27/152226](https://www.hamayanhamayan.com/entry/2017/02/27/152226)

[https://www.hamayanhamayan.com/entry/2017/03/20/234711](https://www.hamayanhamayan.com/entry/2017/03/20/234711)


