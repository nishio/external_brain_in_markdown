
サイズ3000の数値の列Aが与えられる。そのすべての部分列Tについて、Tの部分列であって、要素の和が与えられたSであるようなものの個数を数え上げよ、という問題。[問題](https://atcoder.jp/contests/abc169/tasks/abc169_f)

すべての部分集合について考えると2の3000乗なのでもちろん無理。小さいサンプルデータについてDPで考える。2,2,4とS=4について。
![image](https://gyazo.com/6d14a1c740a68c6be7f9b2814efabf15/thumb/1000)
2,2で4になる経路と、4が1個で4になる経路がある。それぞれの経路の太さがどう決まるか考える。
![image](https://gyazo.com/3a85007b49caba15b0f55fc8d63688f0/thumb/1000)
素朴にコードにする
python

```
import numpy as np
P = 998244353

# N = 10
# S = 10
# AS = list(map(int, "3 1 4 1 5 9 2 6 5 3".split()))
N, S = map(int, input().split())
AS = list(map(int, input().split()))
DP = np.zeros((S + 1, N + 1), dtype=np.int64)
DP[0, 0] = 1
# print(DP)

for i in range(N):
    for j in range(S + 1):
        v = DP[j, i] * 2
        if AS[i] <= j:
            v += DP[j - AS[i], i]
        DP[j, i + 1] = v % P

# print(DP)
print(DP[S, N])
```

サンプルデータに正解したのでサブミットしたが13 TLE
jについてループを回さずにnumpyでまとめて計算することが可能だとは思うけど、考えるのが面倒なので[[numba]]で解決

AC [https://atcoder.jp/contests/abc169/submissions/14608435](https://atcoder.jp/contests/abc169/submissions/14608435)
