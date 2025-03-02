
[S - Digit Sum](https://atcoder.jp/contests/dp/tasks/dp_s)
- ある数K以下の自然数で、条件を満たすものがいくつあるか、という問題
    - 素朴にK個の数を調べることはKがやたらでかいのでできない前提
    - [[桁DP]]
    - > 桁DPはもらうDPよりも配るDPの方が圧倒的に書きやすい
        - [EDPC解説 M～T - kyopro_friends’ diary](https://kyopro-friends.hatenablog.com/entry/2019/01/12/231035)
        - なるほど、以前試してバグらせた時はもらう実装でやってた
- まずはシンプルに「K以下の自然数の個数を数え上げる」をDPで考える
    - ![image](https://gyazo.com/c9063ac33df020121c1f8d9ce839578a/thumb/1000)
    - 57以下の自然数の数を数えている
        - ゼロを含むので「57未満が57個、イコールが1個」となっている
    - 「先頭i桁」を定義域とし、そこまでで「K以下である数」「イコールKである数」の個数を値とするDP
        - ところで「イコールKである数」は常に1なのだからテーブルで持つ必要はないよね
        - 解説などではテーブルで持ってるものが多くて、その方が複雑な問題だと実装の都合が良いことがあるのかな
        - 今回の問題では追加の条件「Dで割り切れる」のチェックのためにDで割ったあまりごとに数え分けているが、僕の実装では「イコールK」にはテーブルを用意しなかった

python

```
def solve(N, D):
    less = [0] * D
    equal = 0
    for digit in N:
        new_less = [0] * D
        for new_digit in range(10):
            for d in range(D):
                new_less[(d + new_digit) % D] += less[d]
            if new_digit < digit:
                new_less[(equal + new_digit) % D] += 1
        for d in range(D):
            new_less[d] %= MOD
        less = new_less
        equal += digit
        equal %= D

    ret = less[0]
    ret -= 1  # for x = 0
    if equal == 0:  # for x = N
        ret += 1
    return ret % MOD
```



old version
python

```
def solve(K, D):
    K = [x - ord("0") for x in K]
    N = len(K)
    less = [[0] * D for i in range(N + 1)]
    border = 0
    for i in range(N):
        for j in range(10):
            for d in range(D):
                less[i][(d + j) % D] += less[i - 1][d]
                less[i][(d + j) % D] %= MOD
            if j < K[i]:
                less[i][(border + j) % D] += 1
        border += K[i]
        border %= D

    ret = less[N - 1][0] - 1
    ret += (border == 0)
    return ret % MOD
```


[https://atcoder.jp/contests/dp/submissions/15082801](https://atcoder.jp/contests/dp/submissions/15082801)
