---
title: "DP J"
---

from [[動的計画法]]
- 問題文[J - Sushi](https://atcoder.jp/contests/dp/tasks/dp_j)
    - 確率的遷移を繰り返して終状態に至るまでの所要時間を求める問題
    - 状態を定義域とし、所要時間期待値を値とする[[期待値DP]]

[[DP_J]]
- [[順序のない列は多重集合]]
    - なんらかの列を扱う問題で、その列の任意の要素を入れ替えても問題に影響ない場合、順序を持った列であることは問題に必要ではない
        - 列の長さがNで、値域がMの時、順序付きではM^N
        - 順序を奪うと[[多重集合]]になり、値ごとの個数で持てばよいのでN^M
        - この問題の場合4通りの値を取るものが100個あるので素朴にやると4^100だが、これが100^4になって格段に狭くなる
- [[期待値DP]]
    - 「期待値DP」は「[[所要時間期待値DP]]」とでも言ったほうが明確になりそうな概念
        - 状態を定義域として、確率を値とする、いわゆる「確率分布」が、1ステップの操作で確率的遷移をして別の分布に変わっていく時に、ある終状態に到達するまでの時間の期待値を求める問題。
        - 素朴に1ステップの更新を繰り返すのではなく、値として「終状態に至るまでの時間の期待値」を持たせて、終状態ではその値が0であることから計算していって始状態の期待値を得るDP
- もっと簡単な問題として「4つの飛び石があって、1/2の確率で次の石に移る、ゴールにたどり着く時間の期待値は？」を考える
    - ![image](https://gyazo.com/baf9dfe526c87ec53abf6f66fa139c33/thumb/1000)
    - 所要時間の期待値を値とするDPを考える
    - aから1ステップ後には、1/2でa、1/2でbにいる
        - 確率を掛けて足し合わせたものが「aの1ステップ後の期待値」
        - 式の両辺にaが出てくる
            - 1/2の確率で自己遷移するから
            - 整理すると、bからaを求める式が得られる
- 今回の問題における遷移
    - ![image](https://gyazo.com/378d95d81f847f835f305597f00c264f/thumb/1000)

- 素朴に実装すると12TLE
python

```
def solve(N, AS):
    "void()"
    from collections import Counter
    count = Counter(AS)
    expect = {}
    expect[(0, 0, 0)] = 0

    def f(a, b, c):
        if (a, b, c) in expect:
            return expect[(a, b, c)]
        p = 1.0
        if a > 0:
            p += f(a - 1, b, c) * a / N
        if b > 0:
            p += f(a + 1, b - 1, c) * b / N
        if c > 0:
            p += f(a, b + 1, c - 1) * c / N
        p *= N / (a + b + c)

        # debug("f: a,b,c,p", a, b, c, p)
        expect[(a, b, c)] = p
        return p

    return f(count[1], count[2], count[3])
```


少し書き直してAC
python

```
def solve(N, AS):
    from collections import Counter
    count = Counter(AS)
    expect = [[[-1] * (N + 1) for i in range(N + 1)] for j in range(N + 1)]
    expect[0][0][0] = 0

    def f(a, b, c):
        p = N
        if a > 0:
            v = expect[a - 1][b][c]
            if v == -1:
                v = f(a - 1, b, c)
            p += v * a
        if b > 0:
            v = expect[a + 1][b - 1][c]
            if v == -1:
                v = f(a + 1, b - 1, c)
            p += v * b
        if c > 0:
            v = expect[a][b + 1][c - 1]
            if v == -1:
                v = f(a, b + 1, c - 1)
            p += v * c
        p /= (a + b + c)

        # debug("f: a,b,c,p", a, b, c, p)
        expect[a][b][c] = p
        return p

    return f(count[1], count[2], count[3])
```

