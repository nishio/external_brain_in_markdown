---
title: "PAST2M"
---

from [[第二回 アルゴリズム実技検定]]
![image](https://gyazo.com/b74deda81b8400cfd3e8c683aff07100/thumb/1000)
[M - 食堂](https://atcoder.jp/contests/past202004-open/tasks/past202004_m)

PAST2M
- 考えたこと
    - 好きな料理が0の時は0
    - それ以外は好きな料理が出たタイミングを起点として周期Dのパターンになる
        - LをDで割れば良い
    - しかしN人の社員それぞれに周期Dのパターンを計算したら10^10で間に合わない、どうすれば良いのか
- 公式解説
    - ![image](https://gyazo.com/c60e3ee7a911c22c643bb530acf812c6/thumb/1000)
- 改めて考えたこと
    - Lは社員によらず一定
    - 次に同じ好きなメニューが出る日がわかれば、間に何回好きでないメニューを食べるかはわかる
    - Tjは人によって異なり、10^9
        - 線形より小さいオーダーでの処理が必要
        - ダブリングで対数オーダーにする
    - 好きな料理をx回食べた時の、食べた回数の総和f(x)をダブリングしてf(x)=yの時のxを求める問題
        - [[単調増加なので二分探索で逆関数できる]]
- 実装
    - 仕様が複雑なので頭の整理のためにまず素朴に実装
    - sample AC:
python

```
def solve(D, L, N, CS, KFTS):
    for K, F, T in KFTS:
        F -= 1  # 1-origin to 0-origin
        ret = 0
        if CS[F % D] == K:
            ret = 1
        countdown = T - 1
        cur = F
        prev = cur
        while countdown:
            cur += 1
            if CS[cur % D] == K:
                ret += 1
                prev = cur
                countdown -= 1
            elif cur - prev == L:
                prev = cur
                countdown -= 1
        print(ret)
```

    - 余りを取らなくてREとかFが1オリジンなの忘れてWAとかした
    - このwhile countdownが10^9なのが問題
    - 解説では次の好きな料理までを1ステップとしてダブリングしてたけど、どうせダブリングするなら1日1ステップで良いのでは？
        - 好きな料理を起点にしないと好きでない料理をいくつ食べる確定しないのでダメ
    - あらかじめ「次の同じ料理」の位置を記録しておき、一度好きな料理が見つかったら飛び飛びに進むバージョン
python

```
def solve(D, L, N, CS, KFTS):
    MAX_C = 10 ** 5
    first = [None] * MAX_C
    prev = [None] * MAX_C
    next = [None] * D
    for i, d in enumerate(CS):
        d -= 1  # to 0-origin
        if first[d] is None:
            first[d] = i
            prev[d] = i
        else:
            next[prev[d]] = i
            prev[d] = i
    for d in range(MAX_C):
        if prev[d] is not None:
            next[prev[d]] = D + first[d]

    for K, F, T in KFTS:
        F -= 1  # 1-origin to 0-origin
        ret = 0
        if CS[F % D] == K:
            ret = 1
        countdown = T - 1
        cur = F
        prev = cur
        while countdown:
            cur += 1
            if CS[cur % D] == K:
                ret += 1
                countdown -= 1
                while True:
                    n = next[cur % D]
                    d = n - cur
                    if d < 0:
                        d += D
                    up = (d - 1) // L + 1
                    if countdown >= up:
                        countdown -= up
                        cur = n
                        ret += 1
                        continue
                    else:
                        countdown = 0
                        break

            elif cur - prev == L:
                prev = cur
                countdown -= 1
        print(ret)
```

    - [diff](https://github.com/nishio/atcoder/commit/30e20a9f78f7581bd1022fb6ad97708f832a8a26)
    - 次はこの「次に進む」の部分をダブリングする
        - 範囲は？
            - 最悪次の皿が隣なら料理の数は+1にしかならないので、10^9になるまでに10^9回必要。
            - 2^30なら確実にオーバーする、`[0, 30)`でOK
    - upの前計算 [diff](https://github.com/nishio/atcoder/commit/58152e4dbc000087e797bbdaa122b1a0da453de1)
        - これが1ステップ
    - ダブリング
        - upsのダブリングにnextの値が必要だと気付いてなくて一度間違った実装をしてしまった
python

```
# doubling
db_next = [next]
db_ups = [ups]
for _i in range(1, 30):
    next = db_next[-1]
    ups = db_ups[-1]
    new_next = []
    new_ups = []
    for i in range(D):
        n1 = next[i] % D
        n2 = next[n1]
        u1 = ups[i]
        u2 = ups[n1]
        new_next.append(n2)
        new_ups.append(u1 + u2)
    db_next.append(new_next)
    db_ups.append(new_ups)
```

    - [[ダブリング→二分探索]]する
python 

```
for i in range(30 - 1, -1, -1):
    up = db_ups[i][cur % D]
    if countdown >= up:
        countdown -= up
        cur = db_next[i][cur % D]
        ret += 2 ** i
```

    - [diff](https://github.com/nishio/atcoder/commit/6997c0a4921fe135107fbc2d7448a56abb4535f9)
- これでもTLEするぞ？(19TLE→10TLE)
    - あ、そうか、好みの料理がない人が10^9で走っちゃうのか
python

```
if first[K - 1] is None:
    print(0)
    continue
```

- それでも4TLE
    - 「好みの料理がF以降に出現する最初の日」をループで求めてるのが良くない
    - これも二分探索するか
    - [AC](https://atcoder.jp/contests/past202004-open/submissions/18976077)
    - [diff](https://github.com/nishio/atcoder/commit/c0ea2d3a7520573486f6552aa6ee854b5cd0fe66)
