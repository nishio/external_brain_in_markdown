
[I - 部品調達](https://atcoder.jp/contests/past201912-open/tasks/past201912_i)
- ![image](https://gyazo.com/c2448c08a7e7e39a1cf0cef3c676a36a/thumb/1000)
- 考えたこと
    - 1000個のセットからいくつか選んで、コスト最小で10個の部品を揃える問題
    - 2^1000は大きすぎるが、1000×2^10なら10^6ぐらいなので余裕
    - 2^10の部分集合を定義域、それを達成する最小コストを値域とするDP
    - 空集合を0、他をINFで初期化してセットごとにchmin
- 公式解説OK
- AC
python

```
def solve(N, M, SS, CS):
    INF = 9223372036854775807
    table = [INF] * (2 ** N)
    table[0] = 0
    SS = [int(s.replace("Y", "1").replace("N", "0"), 2) for s in SS]
    for i in range(M):
        s = SS[i]
        for src in range(2 ** N):
            dst = s | src
            table[dst] = min(table[dst], table[src] + CS[i])
    ret = table[2 ** N - 1]
    if ret == INF:
        return -1
    return ret
```


- [[bit DP]]
- [[コスト最小化]]

[[第一回 アルゴリズム実技検定]]