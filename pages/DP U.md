---
title: "DP U"
---

[U - Grouping](https://atcoder.jp/contests/dp/tasks/dp_u)
- N個の要素を任意個のグループに分ける、分け方によってスコアが決まり、そのスコアを最大化する問題

- 要素が2個の場合、スコアが正なら同じグループ、負なら違うグループにすれば良い
    - しかし3個目の要素を追加した時にこれの他の要素へのつながりが強ければ「やっぱり同じグループに入れた方がよかった」となる
    - k-1個のグループわけごとのスコアをもとに、それに1つ追加した時のスコアを求めていくDPかな？
        - それだと各グループわけが同一視できないので指数的オーダーか？
        - あ、Nが最大16か。それでいいのかも。
        - この方法だと、最初の要素が1つのグループになり、次の要素がそこに参加するか新しいグループになるかの2通り、3つ目の要素は…
            - ![image](https://gyazo.com/6f38fa909ae869e3d950faf49d9fd560/thumb/1000)
            - うーん、このグループ分けを更新していくデータ構造大変そう
- 解説を読むと逆に「与えられた集合を2つに割る」というアプローチをしていた、なるほど
    - [EDPC解説 U～Z - kyopro_friends’ diary](https://kyopro-friends.hatenablog.com/entry/2019/01/12/231106)
- 全体集合からスタートして[[メモ化再帰]]で戻りに計算
    - 与えられた集合が要素数1ならスコア0
    - 与えられた集合を分割しない選択肢もあり
    - 与えられた集合の外には影響しないので最大スコアだけ返せば良い
- グループごとのスコア
    - どんな部分集合Sもどうせ1回は使うので、最初に全部の部分集合に対して計算してキャッシュしよう
    - この計算プロセス自体をDPできそうな気がする
        - やらなくてもACしたのでなってない

グループごとのスコア計算
- 与えられた集合の要素に対する2重ループ
python

```
def calcScore(S):
    debug("enter calcScore: S", S)
    x = S
    ret = 0
    i = 0
    while x:
        if x & 1:
            debug(": i", i)
            for j in range(i):
                if (S >> j) & 1:
                    debug(": i, j, M[i,j]", i, j, M[i, j])
                    ret += M[i, j]
        x //= 2
        i += 1
    debug("leave calcScore: ret", ret)
    return ret
groupScore = [calcScore(i) for i in range(1 << N)]
```


与えられた集合の[[部分集合列挙]]
python

```
def solve(S):
    x = S
    while x > 0:
        print(f"{x:08b}")
        x = (x - 1) & S
```

:

```
>>> solve(14)
00001110
00001100
00001010
00001000
00000110
00000100
00000010

>>> solve(10)
00001010
00001000
00000010
```


組み合わせるとこんな感じ。
- サンプルケースに対して正しい答えを出すけどTLEしそう。雑にキャッシュしてるのをもう少し真面目に書き直す必要がある。
python

```
def solve(N, M):
    FULLBIT = (1 << N) - 1

    def calcScore(S):
        # debug("enter calcScore: S", S)
        x = S
        ret = 0
        i = 0
        while x:
            if x & 1:
                # debug(": i", i)
                for j in range(i):
                    if (S >> j) & 1:
                        # debug(": i, j, M[i,j]", i, j, M[i, j])
                        ret += M[i * N + j]
            x //= 2
            i += 1
        # debug("leave calcScore: ret", ret)
        return ret
    groupScore = [calcScore(i) for i in range(1 << N)]
    # debug(": groupScore", groupScore)

    from functools import lru_cache
    @lru_cache(maxsize=None)
    def sub(S):
        ret = groupScore[S]
        x = (S - 1) & S
        while x > 0:
            y = (~x) & S
            v = sub(x) + sub(y)
            if v > ret:
                ret = v
            x = (x - 1) & S
        return ret

    return sub(FULLBIT)
```


キャッシュを書き直して十分AC
python

```
    table = [None] * (1 << N)

    def sub(S):
        ret = table[S]
        if ret != None:
            return ret
        ret = groupScore[S]
        x = (S - 1) & S
        while x > 0:
            y = (~x) & S
            v = sub(x) + sub(y)
            if v > ret:
                ret = v
            x = (x - 1) & S
        table[S] = ret
        return ret
```

AC [https://atcoder.jp/contests/dp/submissions/15101926](https://atcoder.jp/contests/dp/submissions/15101926)
