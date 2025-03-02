---
title: "ABC186E"
---

from [[ABC186]]
ABC186E
- ![image](https://gyazo.com/90585b907bd02b760801e90adbe4c60d/thumb/1000)
- [E - Throne](https://atcoder.jp/contests/abc186/tasks/abc186_e)
- 要するに $S + K n \equiv 0 \pmod{N}$となるnを求めよという問題
    - n = -S / Kすればいい
    - mod Nなので割り算には逆元の計算が必要
- Kの[[mod Pでの逆元]]を求めれば良い
    - が、普段使ってたフェルマーの小定理を使うコードはPが素数でない時に正しくない値を返す
    - サンプルに入ってた3のmod 10での逆元がまさにこれ。1になってしまう。
    - 本当は7: $3 \times 7 = 21 \equiv 1 \pmod{10}$
- [[拡張ユークリッド互除法]]を使って逆元を求める
- この場合もKとPが互いに素であることが必要なので、先にgcdして1でないなら割っておく
    - Sを割り切れない時は解なし
python

```
def solve(N, S, K):
    from math import gcd
    g = gcd(K, N)
    if g > 1:
        if S % g != 0:
            return -1
        N //= g
        K //= g
        S //= g

    invK = mod_inverse_ee(K, N)
    ret = (N - S) * invK % N

    return ret
```

- [[Pが素数でないmod P]]
- [https://twitter.com/drken1215/status/1340338865622564864?s=21](https://twitter.com/drken1215/status/1340338865622564864?s=21)
    - [[中国剰余定理]]
