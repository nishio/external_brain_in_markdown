---
title: "DP T"
---

[T - Permutation](https://atcoder.jp/contests/dp/tasks/dp_t)
- 与えられた大小関係を満たすように数を並べる方法が何通りあるかを数え上げる問題
- 「まだ使ってない数の集合」を定義域とするDPかな？
    - 集合のサイズが3000と大きいので無理
- 何かを同一視することによって定義域を狭められないか？
    - ![image](https://gyazo.com/cf77e332e55be1555ffab63ac2e210de/thumb/1000)
    - この二つのシチュエーションのどちらでも「選択肢が3つある」ということに変わりがない
    - というわけで「直前に選択された数よりも大きいものが何個、小さいものが何個」を定義域にする
- 探索の末端はどこか？
    - 数が残り1個になった状態
    - 「残り1個状態」をあらかじめ列挙してから「残りk-1個状態の値を使って残りk個状態を求める」というDP


![image](https://gyazo.com/15d46557ea961335ad637bf01a487a4a/thumb/1000)

まずはN=2の時に正しく動くコードを作る
python

```
def solve(N, lessthan):
    # init
    # f("<", lower=0, upper=1) = 1, f("<", 1, 0) = 0
    k = 1
    table = [0] * (k + 1)
    if lessthan[-1]:
        for i in range(k + 1):
            table[i] = k - i
    else:
        for i in range(k + 1):
            table[i] = i

    return sum(table)
```


次にN=3の時に正しく動くコードを作る
python

```
def solve(N, lessthan):
    k = 1
    table = [0] * (k + 1)
    if lessthan[-1]:
        for i in range(k + 1):
            table[i] = k - i
    else:
        for i in range(k + 1):
            table[i] = i

    if N > 2:
        k = 2
        newtable = [0] * (k + 1)
        if lessthan[-2]:
            for i in range(k + 1):
                for j in range(k - i):
                    newtable[i] += table[j + i]
        else:
            for i in range(k + 1):
                for j in range(i):
                    newtable[i] += table[j]
        table = newtable
    return sum(table)
```


そして一般のNに拡張する。
- これでサンプルコードは全部通る
- サブミットするとTLE
python

```
def solve(N, lessthan):
    k = 1
    table = [0] * (k + 1)
    if lessthan[-1]:
        for i in range(k + 1):
            table[i] = k - i
    else:
        for i in range(k + 1):
            table[i] = i

    for k in range(2, N):
        newtable = [0] * (k + 1)
        if lessthan[-k]:
            for i in range(k + 1):
                for j in range(k - i):
                    newtable[i] += table[j + i]
        else:
            for i in range(k + 1):
                for j in range(i):
                    newtable[i] += table[j]
        table = [x % MOD for x in newtable]
    return sum(table) % MOD
```


ループの中身がようは範囲sumなので累積和を使って高速化する、これでAC
python

```
    for k in range(2, N):
        newtable = [0] * (k + 1)
        acc = [0] + list(accumulate(table))
        if lessthan[-k]:
            for i in range(k + 1):
                # for j in range(k - i):
                #    newtable[i] += table[j + i]
                newtable[i] += acc[k] - acc[i]
        else:
            for i in range(k + 1):
                # for j in range(i):
                #    newtable[i] += table[j]
                newtable[i] += acc[i]
        table = [x % MOD for x in newtable]
```

AC: [https://atcoder.jp/contests/dp/submissions/15098388](https://atcoder.jp/contests/dp/submissions/15098388)
