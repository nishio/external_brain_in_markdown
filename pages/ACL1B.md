
from [[ACL1]]
ACL1B
[B - Sum is Multiple](https://atcoder.jp/contests/acl1/tasks/acl1_b)
- ![image](https://gyazo.com/05e1340235546d99c96be1d91098fd5f/thumb/1000)
- 考えたこと
    - $1 + 2 + \cdots + k = k (k + 1) / 2$なので問題条件はk * (k + 1)  % N = 0
        - 注: mod 2Nが正しい
    - とりあえず素朴に探索して表示し、パターンを見つける
    - Nが素数の時はk=N-1
    - Nが2の累乗の時もk=N-1
    - 異なる素因数に分かれてる時に小さくなる
    - Nの素因数分解fを求めて最大の`m = max([p ** f[p] for p in f])`を得る
    - mで満たさない残りr = N // mを考える
    - nm + 1  もしくはnm - 1がrの倍数であるような最小のnを素朴に探す
        - →これでは問題の求める最小解が得られるとは限らない
    - 方針がダメなのかと思って終了
- 公式解説
    - 上記条件(に似た条件)を満たす解は[[CRT]]で得られる
    - 最大のmについてだけ計算するのではなく、約数全体について行う
        - Nのある約数mについて、r = 2 * N // mとして
            - kはmの倍数、k+1はrの倍数、となるkが存在するか？
                - 存在するためにはmとrが互いに素である必要がある
                - 互いに素である場合には[[中国剰余定理]]の解の存在に帰着する
        - [[約数列挙]]がO(sqrtN)、各約数についてのCRTがO(logN)なので間に合うらしい
- [maspyさんの解説](https://maspypy.com/atcoder-参加感想-2020-09-20acl1)
    - CRTは必要ない
    - $k \equiv 0 \pmod{m}, k \equiv -1 \pmod{r}$ の時 $k = am$とすると
        - $am \equiv -1 \pmod{r}$,
        - $ a \equiv -1 \cdot m^{-1} \pmod{r}$
        - というわけで  ` k = -1 * inv_mod(m, r) * m `で良いから
- CRT version
python

```
def solve(N):
    from math import gcd
    if N == 1:
        return 1
    ret = N - 1
    for n in all_divisor(2 * N, includeN=False):
        m = (2 * N) // n
        if gcd(m, n) != 1:
            continue
        k = crt(0, n, -1, m)
        if k < ret:
            ret = k
    return ret
```

- non-CRT version
python

```
def solve(N):
    if N == 1:
        return 1
    factors = factor(2 * N)
    num_factors = len(factors)
    if num_factors == 1:
        return N - 1
    factors = [p ** factors[p] for p in factors]
    ret = N - 1
    for i in range(2 ** num_factors - 1):
        prod = 1
        j = 0
        while i:
            if i & 1:
                prod *= factors[j]
            j += 1
            i >>= 1

        rest = (2 * N) // prod
        k = (-pow(prod, -1, rest) * prod) % (2 * N)
        if k < ret:
            ret = k

    return ret
```

    - うーむ [AC 21 TLE 21](https://atcoder.jp/contests/acl1/submissions/17258486)
        - 素因数分解が遅いのか、束ね直すところが遅いのか
        - [[素因数分解を O(n^(1/4)) でする]]に置き換えたら通った [51msec](https://atcoder.jp/contests/acl1/submissions/17259156)
    - あとpowが[[mod Pでの逆元]]を求められるのはPython3.8からの割と新しい機能なのでPyPyでは動かなかった
        - `ValueError: pow() 2nd argument cannot be negative when 3rd argument specified`
- 2Nが正しい話
    - Nが6の時1+2+3 = 6なので3が解
    - N だと 2 * 3 mod 6 = 0で2, 3が互いに素なので2と答えてしまう
    - 2N だと 2, 6は 互いに素でなく、3, 4の3を答えて正解
