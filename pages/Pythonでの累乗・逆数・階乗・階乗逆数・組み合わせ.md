---
title: "Pythonでの累乗・逆数・階乗・階乗逆数・組み合わせ"
---

自分が[[ABC171 F]]の時に書いたコードを再利用するために整理してて、ついでに[maspy法](https://maspypy.com/numpyn-mod-p%e3%81%ae%e8%a8%88%e7%ae%97)と速度比較してみたらmaspy法を[[Numba]]でコンパイルしたものが一番速かった。

100万件からの組み合わせテーブル作成が、特定のnに対してワンショットなら35msec、階乗と逆数階乗を先に作って使い回すなら49msec(準備に30msec)

自作のも53msecと割といいとこ言ってると思うんだけどなー。負けは負けです。

その後、maspy法からreshapeと反転を取り除いて33msecになった
python

```
@numba.njit
def makeCombibationTableJointedNoReshapeNumba(N):
    """ make table of C(n, i) for i in [0, N)
    Jointed version of makeFactorialTableMaspy, 
    makeInvFactoTableMaspyOriginal, and makeCombibationTableMaspy.

    >>> list(makeCombibationTableJointedNumba(10000)[:5])
    [1, 10000, 49995000, 616668838, 709582588]

    %timeit makeCombibationTableJointedNoReshapeNumba(K)
    33 ms ± 809 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
    """
    K = math.ceil(math.sqrt(N + 1)) ** 2
    rootK = math.ceil(math.sqrt(K))

    facto = np.arange(K, dtype=np.int64)
    facto[0] = 1
    for i in range(1, rootK):
        facto[i::rootK] *= facto[i-1::rootK]
        facto[i::rootK] %= MOD
    for start in range(rootK, K, rootK):
        end = start + rootK
        facto[start:end] *= facto[start - 1]
        facto[start:end] %= MOD

    invf = np.arange(1, K + 1, dtype=np.int64)
    invf[-1] = getSingleInverseNumba(facto[K - 1])  # inverse of (k-1)!
    for pos in range(rootK - 2, -1, -1):
        invf[pos::rootK] *= invf[pos + 1::rootK]
        invf[pos::rootK] %= MOD

    for end in range(-rootK, -K, -rootK):
        start = end - rootK
        invf[start:end] *= invf[end]
        invf[start:end] %= MOD
    return facto[N] * invf[:N + 1] % MOD * invf[N::-1] % MOD
```



実装
[https://github.com/nishio/atcoder/blob/master/memo/combination.py](https://github.com/nishio/atcoder/blob/master/memo/combination.py)
- Power: 13msec
- Inverse: 47msec
- Factorial: 13msec (K is excluded)
- InvFactorial: 17msec (Need to give (K - 1)!)
- Combination:
    - 35msec (if you need C(n, r) for specific n)
    - 19msec (need f and invf. 13 + 17 + 19 = 49msec)

メモ
- Numbaはcontiguous arrayでないとreshapeできないので[[np.ascontiguousarray]]する
- 逆元を[[フェルマーの小定理]]で求めてるところはNumba的には「floatかな？」となるので[[ユークリッドの互除法]]に変更
- maspy法は[[平方分割]]の一種なのかな
- オリジナルの実装では`[0, K)`
    - 問題条件で「10 ** 6を含む」とされてるケースが多いから`[1, K]`の方が良いのではないか
    - 実装してみたが、この場合n!がn-1に入ってるからバグの元かもなと思った
    - 一回り大きめに作るのが良い
        - 平方数の制約があるのでちょっと面倒
        - 一回り大きくするコードも入れておいた


[https://ikatakos.com/pot/programming_algorithm/number_theory/mod_combination](https://ikatakos.com/pot/programming_algorithm/number_theory/mod_combination)
