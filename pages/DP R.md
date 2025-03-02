---
title: "DP R"
---

[R - Walk](https://atcoder.jp/contests/dp/tasks/dp_r)
- 有向グラフの長さKのパスを数え上げる問題
- 素朴に考えれば長さk-1のパスの数から長さkの数を求めるDP
- だがKが最大10^18という問題条件から、K回繰り返しを行う方法では無理
- 世の中的にはここで「行列の積」「[[繰り返し二乗法]]」と飛躍するんだけどもう少し噛み砕くと
- 「N回同じ処理をする必要があるがO(N)では遅い時にどうするか」という話
    - 二分木的な方法でlog Nにすれば良いよね、となる
    - Nについての処理を N/2についての処理結果を使って高速に演算できればlog Nになる
- これが今回の場合たまたま行列の掛け算になるだけの話

- 素朴に書くとこうなる
    - これはWA
    - なぜかというと要素が最大10^9のサイズ50の行列の掛け算は要素が64ビットの範囲を超えるから。
        - 掛け算してからmodしても手遅れ。
python

```
def solve(N, K, X):
    powK = np.eye(N, dtype=np.int64)
    while K:
        if K & 1:
            powK = powK.dot(X)
            powK %= MOD
        X = X.dot(X)
        X %= MOD
        K //= 2
    return powK.sum() % MOD
```


- 要素を掛け合わせるところまでならまだ60ビットなので、そこでmodをとってから足し合わせる
python

```
def solve(N, K, X):
    def modmul(x, y):
        ret = np.zeros(x.shape, np.int64)
        for i in range(N):
            for j in range(N):
                v = x[i, :] * y[:, j]
                v %= MOD
                ret[i, j] = v.sum() % MOD
        return ret

    powK = np.eye(N, dtype=np.int64)
    while K:
        if K & 1:
            powK = modmul(powK, X)
        X = modmul(X, X)
        K //= 2
    return powK.sum() % MOD
```


[https://atcoder.jp/contests/dp/submissions/15081435](https://atcoder.jp/contests/dp/submissions/15081435)
