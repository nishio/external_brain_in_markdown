---
title: "ACL Beginner Contest"
---

[[AtCoder Library]]を使える問題が出されるコンテスト。

BをケアレスミスしたことにCの提出後に気づき修正、Dを実装してサンプルを通してから提出したもののWAで、Eを見たら[[遅延伝搬セグメント木]]だなと思ったのでそちらを解く。何度か失敗してAC。Dに戻って「これはセグメント木でDPだな」と気づいたが、その時点で残り10分。間に合わず。
![image](https://gyazo.com/cf293b51cdb0f3e61921e381956d2872/thumb/1000)

うわ、あと9ポイントで水色！惜しい！
![image](https://gyazo.com/9dabf4b98969d40e2b5509564cfe5ff0/thumb/1000)

[B - Integer Preference](https://atcoder.jp/contests/abl/tasks/abl_b)
- ![image](https://gyazo.com/f4f4a47bc47a888934ec7935d5699512/thumb/1000)
- ケアレスミスした
    - 大急ぎで直したので不格好な条件式
python

```
A, B, C, D = map(int, input().split())
# if A <= D <= B or A <= C <= B:  # NG
if A <= D <= B or A <= C <= B or C <= A <= D:
    print("Yes")
else:
    print("No")
```

- 落ち着いて考えるとこう
python

```
A, B, C, D = map(int, input().split())
if D < A or B < C:
    print("No")
else:
    print("Yes")
```


[C - Connect Cities](https://atcoder.jp/contests/abl/tasks/abl_c)
- ![image](https://gyazo.com/d392de5b2ccc1dc816648fb819b6adbf/thumb/1000)
- 繋がってる都市の塊がいくつあるか数えて(Xとする)、その一つから残りX-1個に道を引けば良い
- 「繋がってる都市の塊」=[[連結成分]]
- というわけで[[UnionFind]]
python

```
def solve(N, M, edges):
    init_unionfind(N)
    for e in edges:
        unite(e[0] - 1, e[1] - 1)

    s = set(find_root(x) for x in range(N))
    return len(s) - 1
```


[D - Flat Subsequence](https://atcoder.jp/contests/abl/tasks/abl_d)
- ![image](https://gyazo.com/13fcd06d7d09419948c239f846aedff7/thumb/1000)
- どうACLに帰着するのかわからないのでまずは素朴に書く
- 提出したが WA/TLE混じり
    - WAが取れてもTLEだろうし、どう解決するか目処が付いてないので一旦保留してEをやった
- 戻ってきて見直してみて、なるほどこれは[[セグメント木]]で[[動的計画法]]だなと気づいたが、残り10分だった
    - 末尾の値を定義域、最長の長さを値域とする動的計画法
    - [[集めるDP]]
    - i番目の値がAの時、Aの前後K個の値のmaxが「i番目の値をつなげることのできる最も長い列」なので、それに1足したもので更新
    - 下記でサンプルは通る
python

```
def solve(N, K, AS):
    count = [0] * 300_000
    count[AS[0]] = 1
    for i in range(1, N):
        A = AS[i]
        start = max(0, A - K)
        best = max(count[start:A + K + 1])
        count[A] = best + 1
    return max(count)
```

- 点更新範囲maxなのでセグメント木が使える
    - セグメント木バージョン AC
python

```
def solve(N, K, AS):
    MAX_CAPACITY = 300_000
    set_width(MAX_CAPACITY + 10)

    count = [0] * SEGTREE_SIZE
    point_set(count, AS[0], 1, max)
    for i in range(1, N):
        A = AS[i]
        start = max(0, A - K)
        end = min(A + K + 1, MAX_CAPACITY + 1)
        best = range_reduce(count, start, end, max, -INF)
        point_set(count, A, best + 1, max)
    return range_reduce(count, 0, MAX_CAPACITY + 1, max, -INF)
```

    - ハマりポイント
        - Pythonのリストは`count[start:end]`でendが範囲外でも許されるが、セグメント木はそうではない
        - `MAX_CAPACITY`を含むので+1が必要

[E - Replace Digits](https://atcoder.jp/contests/abl/tasks/abl_e)
- ![image](https://gyazo.com/2bd499438884da4227a67110c503b545/thumb/1000)
- 範囲更新するので双対セグメント木かなと思った
- クエリのたびに「20万桁の十進数とみなしてあまりを計算」って処理が走るのは[[範囲縮約]]だから[[遅延伝搬セグメント木]]が適当
- この処理をするための値の二項演算が`(a * 10 + b) % MOD`だと勘違いした
    - 実際には右側の数字の桁数をsizeとして`(a * (10 ** size) + b) % MOD`
    - 二項演算がsizeを引数に取らないので大急ぎで自作ライブラリを手直しした
    - 別解
        - >  E は、(長さ、sum）を持ちました。 (10^n, sum) を持った方が mod pow を使わずに済んで計算量が良いと思います。
            - [twitter @maspy_stars](https://twitter.com/maspy_stars/status/1309859601483849733)

- 20万桁の十進数になるので`11111111`や`10000000`のあまりを前計算しておく
python

```
def main():
    # parse input
    N, Q = map(int, input().split())
    set_width(N + 1)

    value_unity = 0
    value_table = [value_unity] * SEGTREE_SIZE
    value_table[NONLEAF_SIZE:NONLEAF_SIZE + N] = [1] * N

    action_unity = None
    action_table = [action_unity] * SEGTREE_SIZE

    cache11 = {}
    i = 1
    p = 1
    step = 10
    while i <= N:
        cache11[i] = p
        p = (p * step + p) % MOD
        step = (step * step) % MOD
        i *= 2

    cache10 = {0: 1}
    i = 1
    p = 10
    while i <= N:
        cache10[i] = p
        p = (p * 10) % MOD
        i += 1

    def action_force(action, value, size):
        if action == action_unity:
            return value
        # return int(str(action) * size)
        return (cache11[size] * action) % MOD

    def action_composite(new_action, old_action):
        if new_action == action_unity:
            return old_action
        return new_action

    def value_binop(a, b, size):
        # return (a * (10 ** size) + b) % MOD
        return (a * cache10[size] + b) % MOD

    full_up(value_table, value_binop)
  
    for _q in range(Q):
        l, r, d = map(int, input().split())
        lazy_range_update(
            action_table, value_table, l - 1, r, d,
            action_composite, action_force, action_unity, value_binop)

        ret = lazy_range_reduce(
            action_table, value_table, 0, N, action_composite, action_force, action_unity,
            value_binop, value_unity)
        print(ret)
```

- [[平方分割]]で解いたとTwitterに書いてる人がいる

F
- 頻度を数えて[[畳み込み]]？
- [[包除原理]]を使ってDP？
- [https://www.hamayanhamayan.com/entry/2020/09/27/013201](https://www.hamayanhamayan.com/entry/2020/09/27/013201)
- [https://kmjp.hatenablog.jp/entry/2020/09/26/1030](https://kmjp.hatenablog.jp/entry/2020/09/26/1030)
