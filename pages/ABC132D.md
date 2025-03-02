---
title: "ABC132D"
---

[D - Blue and Red Balls](https://atcoder.jp/contests/abc132/tasks/abc132_d)
- ![image](https://gyazo.com/b40880b288c4dd49649f7ecc52b89ecc/thumb/1000)
- 考えたこと
    - 要するにK個の青いボールをi個の非連続なグループにする並べ方を数え上げたい
    - グループの間には1個以上の赤いボールが入る
    - K個の青いボールをi個の非連続なグループにする
        - ![image](https://gyazo.com/95d89bbd307f278fd1788557b7742f0e/thumb/1000)
        - $b_i = \binom{K-1}{i-1}$
    - N-K個の赤いボールはi+1個のグループに分かれる、ただし両端は0になりうる
        - ![image](https://gyazo.com/7e203a9a37997fafc1062cd78ebda967/thumb/1000)
        - $r_i = \binom{N-K+1}{i}$
    - あとはこれをK件計算すれば良い
        - 2000までの前計算をして高速化する
- 公式解説
    - 方針OK
    - Kが2000と小さいので前計算せずに[[パスカルの三角形]]でもOKとのこと
- AC
    - 上記方針で素朴に実装するとriの計算でN - K - 1 < i になりうる。
        - 数学的には0だが、コンビネーションの実装が想定してなくて、不正な値を返してWAした
        - ケアレスミスで時間を溶かさないようにライブラリの側でケアした
python

```
def main():
    N, K = map(int, input().split())
    MOD = 1_000_000_007
    c = Combination(N, MOD)
    for i in range(1, K + 1):
        r = c.comb(K - 1, i - 1)
        r *= c.comb(N - K + 1, i)
        r %= MOD
        print(r)
```


