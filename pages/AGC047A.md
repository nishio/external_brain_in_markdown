---
title: "AGC047A"
---

AC
[A - Integer Product](https://atcoder.jp/contests/agc047/tasks/agc047_a)
![image](https://gyazo.com/e7dec806a945dce731880ce2d2c75d8e/thumb/1000)
- 浮動小数点数を使うのは避けて10^9倍して整数にした
    - 問題条件は「整数を掛けて10^18の倍数になるか」になる
    - それぞれの数を2で何回割れるか(P2)、5で何回割れるか(P5)、を計算しておく
    - `P2[i] + P2[j] > 17 and P5[i] + P5[j] > 17`なら「掛けて10^18の倍数になる」
python

```
def solve1(N, AS):
    ret = 0
    P2 = []
    P5 = []
    for i in range(N):
        p2 = 0
        p5 = 0
        x = AS[i]
        while x % 2 == 0:
            p2 += 1
            x //= 2
        while x % 5 == 0:
            p5 += 1
            x //= 5
        P2.append(p2)
        P5.append(p5)

    for i in range(N):
        for j in range(i + 1, N):
            if P2[i] + P2[j] > 17 and P5[i] + P5[j] > 17:
                ret += 1
    return ret
```


これで小さいデータに対してはACするが、大きいとTLEになる
- 数が最大20万個あるので、一個ずつ比べる方法では百億オーダーだからTLEになる
    - Nの二重ループがあるのがいけない
    - 前処理をすることでこれを一重ループで済ませる
    - つまり`P2[i], P5[i]`が与えられた時に「`P2[i] + P2[j] > 17 and P5[i] + P5[j] > 17`を満たすjの数」がループを回さずにわかれば良い
    - →[[頻度表]]を作る
- 解説によればそれだけでもACになりそう
    - 頻度分布表の幅は高々19
        - 18乗以上は区別する必要がないから
    - 計算回数は20万×400程度なので十分狭い
- だけど僕は気づかないでさらに工夫した
    - あらかじめ[[累積和]]を計算しておくことで「`P2[i] + P2[j] > 17 and P5[i] + P5[j] > 17`を満たすjの数」が頻度表でのループすらなく求められる
    - Numpyだと[[二次元配列の累積和]]も簡単
python

```
for i in range(19, 0, -1):
    P[i - 1] += P[i]
for i in range(19, 0, -1):
    P[:, i - 1] += P[:, i]
```

- これで一重ループで求められるようになる
python

```
for i in range(N):
    ret += P[18 - P2[i], 18 - P5[i]]
```

- だが、これだと正しい答えにならないので修正が必要
    - まず、P2もP5も9以上の数については「自分自身」をペアにカウントしてしまっているのでそれを引く
    - 残りに関してはijペアとjiペアを両方カウントしているので2で割る
- これで正解になる

python

```
def solve(N, AS):
    import numpy as np
    ret = 0
    P2 = []
    P5 = []
    P = np.zeros((20, 20), dtype=np.int)

    for i in range(N):
        p2 = 0
        p5 = 0
        x = AS[i]
        while x % 2 == 0:
            p2 += 1
            x //= 2
        while x % 5 == 0:
            p5 += 1
            x //= 5
        if p2 > 18:
            p2 = 18
        P2.append(p2)
        P5.append(p5)
        P[p2, p5] += 1

    for i in range(19, 0, -1):
        P[i - 1] += P[i]
    for i in range(19, 0, -1):
        P[:, i - 1] += P[:, i]

    for i in range(N):
        ret += P[18 - P2[i], 18 - P5[i]]
    ret -= P[9, 9]
    ret //= 2
    return ret
```


