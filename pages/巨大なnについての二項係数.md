
巨大なn(10^9)について二項係数を求める場合、n!の計算がO(n)なので間に合わない
$\binom{n}{k} = \frac{n!}{k!(n-k)!} = \frac{n!}{(n-k)!} \frac{1}{k!}$
と変形すればそれぞれはO(k)で求められる

実装例
python

```
def naive_comb(n, k, MOD=MOD):
    assert n >= 0
    assert k >= 0
    if n < k:
        return 0
    k = min(k, n - k)
    a = 1
    b = 1
    for i in range(k):
        a *= (n - i)
        a %= MOD
        b *= (i + 1)
        b %= MOD
    return (a * mod_inverse(b, MOD)) % MOD
```

- mod_inverseについては [[mod Pでの逆元]]

[[巨大なnについての組み合わせ]]
from [[mod Pでの組み合わせ]]
