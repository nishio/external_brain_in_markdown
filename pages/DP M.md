
[M - Candies](https://atcoder.jp/contests/dp/tasks/dp_m)
![image](https://gyazo.com/7f00d3569b97262049eab2547f73d1ad/thumb/1000)

- 分配の数え上げ問題
- DP合流時の足し算が重たい
    - [[累積和]]を事前に求める

素朴な解法、これで最後以外のサンプルは通る
python

```
def solve(N, K, XS):
    table = [0] * (K + 1)
    for i in range(XS[0] + 1):
        table[i] = 1

    for i in range(1, N):
        v = 0
        newtable = [0] * (K + 1)
        for j in range(K + 1):
            v = 0
            for k in range(XS[i] + 1):
                if j - k < 0:
                    break
                v += table[j - k]
                v %= MOD

            newtable[j] = v
        table = newtable

    return table[K]
```


シンプルなもので何がいけないかというと足し算のループなので、事前に累積和を求める
python

```
def solve(N, K, XS):
    table = [0] * (K + 1)
    for i in range(XS[0] + 1):
        table[i] = 1

    for i in range(1, N):
        v = 0
        newtable = [0] * (K + 1)
        accum = [0] * (K + 1)
        acc = 0
        for j in range(K + 1):
            acc += table[j]
            accum[j] = acc

        for j in range(K + 1):
            v = accum[j]
            k = j - XS[i] - 1
            if k >= 0:
                v -= accum[k]

            newtable[j] = v % MOD
        table = newtable

    return table[K]
```


