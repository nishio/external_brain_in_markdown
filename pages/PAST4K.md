---
title: "PAST4K"
---

from [[第四回 アルゴリズム実技検定]]
PAST4K
[K - 転倒数](https://atcoder.jp/contests/past202010-open/tasks/past202010_k)
- 考えたこと
    - [[転倒数]]
        - 結合した時にどうなるか考察
            - 結合した列の転倒数はそれぞれの転倒数と頻度表から求められる [[ACLPC L]]
        - 結合する前に単独で計算する時のnが最大で10^5だ
        - どうするのか
            - [https://ikatakos.com/pot/programming_algorithm/dynamic_programming/inversion](https://ikatakos.com/pot/programming_algorithm/dynamic_programming/inversion)
            - [[フェニック木]]らしい
        - サンプルは通ったがWA
            - TLEもしてる
        - 1ずらしてWAが消えるかテスト
            - だめ
        - あまりが10^9だった！
    - WA消えたが3TLE
        - インライン展開した、これでだめならダメ
        - ダメだった
    - これ以上に何ができるのか
        - そもそも3×10^5なのに、なぜ5秒もあるのがタイムアウトするのか
    - 30万だとダメだが10万ずつだとOKなのか？
        - それでも3TLE
    - Cythonにしてみたけどダメ
    - C++で書くべきか？
- 公式解説
    - 方針は良い
    - 同じ列が繰り返し使われる時に毎回フェニック木で転倒数を求めていたのがよくない
        - 転倒数と頻度表を前処理すべきだった
    - 列の長さの和が小さく抑えられているのは、前処理でフェニック木を使うのはTLEしないが、クエリのたびに使うとクエリが長い列ばかり選ぶ場合があってNGという意図
- AC
python

```
def solve(K, seqs, Q, BS):
    MOD = 10 ** 9
    N = 20

    invs = []
    freqs = []
    for i in range(K):
        init(N)
        freq = [0] * 21
        inv = 0
        for a in seqs[i]:
            bit_add(a, 1)
            inv += bit_sum(N) - bit_sum(a)
            freq[a] += 1
        invs.append(inv)
        freqs.append(freq)

    ret = 0
    freq = [0] * 21
    for b in BS:
        ret += invs[b - 1]
        f = freqs[b - 1]
        for i in range(1, 21):
            for j in range(i + 1, 21):
                ret += f[i] * freq[j]

        for i in range(1, 21):
            freq[i] += f[i]
        ret %= MOD

    return ret
```


