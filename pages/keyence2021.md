
[キーエンス プログラミング コンテスト 2021 - AtCoder](https://atcoder.jp/contests/keyence2021) ARC相当の難易度
A-Cの3問でした

![image](https://gyazo.com/1cf13ccfd7b034a59134adbb8aa0b42a/thumb/1000)


[A - Two Sequences 2](https://atcoder.jp/contests/keyence2021/tasks/keyence2021_a)
![image](https://gyazo.com/8886c1232049da6b710c42699eb6acb4/thumb/1000)
- $c_n = \max a_ib_j[i\le j\le n]$を求める問題 ([[Iverson bracket]]記法)
- $c_n = \max (c_{n-1},  \max a_ib_n [i\le n])$
- $c_n = \max (c_{n-1},  b_n \max a_i [i\le n])$
- というわけで $\max a_i [i\le n]$を別途保存しておけばOK
python

```
def main():
    N = int(input())
    AS = list(map(int, input().split()))
    BS = list(map(int, input().split()))
    maxAS = []
    x = 0
    for i in range(N):
        x = max(x, AS[i])
        maxAS.append(x)

    ret = AS[0] * BS[0]
    print(ret)
    for i in range(1, N):
        ret = max(ret, maxAS[i] * BS[i])
        print(ret)
```


[B - Mex Boxes](https://atcoder.jp/contests/keyence2021/tasks/keyence2021_b)
![image](https://gyazo.com/399ab72dbb56393a66ef66e1ef97034c/thumb/1000)
- 同じ箱に同じ値を入れてもメリットがない
- 数値が飛んでたら結果に影響しない
- というわけで「0から順に連続して入れられるだけ入れる」が最適解になる貪欲法
- 箱の数の制限を忘れてて一度WAになった: (1)の`K > 0`
python

```
def main():
    N, K = map(int, input().split())
    AS = list(map(int, input().split()))
    from collections import Counter
    count = Counter(AS)
    ret = 0
    while count[0] > 0 and K > 0:  # (1)
        i = 0
        K -= 1
        while count[i] > 0:
            ret += 1
            count[i] -= 1
            i += 1

    print(ret)
```


[C - Robot on Grid](https://atcoder.jp/contests/keyence2021/tasks/keyence2021_c)
![image](https://gyazo.com/e60412189e8d57b2f1c1e23ba8897f9c/thumb/1000)
- 最初、図の間違った方のDPをしてサンプルが合わなくて悩んだ
    - ![image](https://gyazo.com/d77469b7257adfbca3f257a13f5e8b0e/thumb/1000)
    - 例えば＊を通らない経路は上のDPだと最終的な答えに1として出されるわけなのだが、＊がM個あるなら3^Mになるのが正しい
    - 最終的に何で割って辻褄を合わせればいいのかも一度間違えたがサンプルが親切なのでよく見ればよい
        - サンプル1の場合、ゴールまでの遷移が2回、＊が1つなので、1回余分だから3^1で割る
        - サンプル2の場合、遷移が4回、＊が4つなので3^0で割る
    - REが出てるのはpowに負の値を入れられるのがPython3.8からなのを忘れてたせい see [[mod Pでの逆元]]
    - タプルをキーにした辞書を使っててTLEしたので、配列に変えた。
        - W+2は、1オリジンなのと、端で条件分岐しないで良いように1マス広げとくのの組み合わせ
python

```
def main():
    MOD = 998_244_353
    H, W, K = map(int, input().split())
    CS = [0] * ((H + 2) * (W + 2))
    for _k in range(K):
        h, w, c = input().strip().split()
        CS[(int(h) * (W + 2) + int(w))] = ord(c)

    table = [0] * ((H + 2) * (W + 2))
    v = table[1 + (W + 2)] = 1
    for h in range(1, H + 1):
        for w in range(1, W + 1):
            pos = h * (W + 2) + w
            v = table[pos] % MOD
            c = CS[pos]
            if c == 88:  # "X":
                table[pos + 1] += v * 3
                table[pos + (W + 2)] += v * 3
            elif c == 68:  # "D":
                table[pos + (W + 2)] += v * 3
            elif c == 82:  # "R":
                table[pos + 1] += v * 3
            else:
                table[pos + 1] += v * 2
                table[pos + (W + 2)] += v * 2

    ret = table[H * (W + 2) + W] % MOD
    LEN = (H + W - 2)
    NEGK = H * W - K
    ret *= pow(3, (MOD - 1 - (LEN - NEGK)), MOD)
    ret %= MOD
    print(ret)
```


[D - Choosing Up Sides](https://atcoder.jp/contests/keyence2021/tasks/keyence2021_d)
- ![image](https://gyazo.com/b2e3f90a7532cacff62fc8ed74d62a72/thumb/1000)

- 考えたこと
    - 8人を半分に分けて対戦させる時、1番の人と同じチームになる人が3人いて、それらの人の「同じだった回数」は1増えるので、1番以外の全員が同じ「1番と同じチームだった回数」になるのは3×7の21回目
        - 間違いです
            - 7箇所のうち3箇所が1であるようなベクトルを7つ足し合わせてすべて3にすることができればよい
- 終了後Twitter
    - [[双対ベクトル]] [src](https://twitter.com/ngtkana/status/1350449811309305856?s=21)
    - [E - Odd Sum Rectangles](https://atcoder.jp/contests/hitachi2020/tasks/hitachi2020_e)のN=Mのときと大体同じ問題 [src](https://twitter.com/titia_til/status/1350443154089025537)
    - 再帰 [src](https://twitter.com/SSRS_cp/status/1350442817785479170)
    - [[アダマール行列]] [src](https://twitter.com/nullkara/status/1350470699400400896?s=21) [src](https://twitter.com/kyopro_friends/status/1350449299272790017?s=21)
    - D: N = 3だったら11110000 11001100 10101010 を作ってこれらを1以上選んでxor [src](https://twitter.com/poyothon/status/1350443900259876870)
        - なるほど
        - 同じ値の連続が$2^i (0 \le i < N)$ であるようなものがN通り作れる
        - これらの値のXORは、それぞれを選択するかどうかの$2^N$個あって、00000000以外はすべて1の個数が4個($2^{N-1}$)
        - この集合はXORについて閉じている(0が単位元)
        - 「同じチームであった回数」は「XORした値の0である桁の数」なので、異なるものをXORした時に0である桁の数が変わらないこの性質が都合が良い
- コンテスト後実装
    - 同じ値の連続が$2^i (0 \le i < N)$ であるようなものをN通り作る
        - なおPythonは256ビットの整数も問題なくビット演算できる
    - このN個をXORして作られる値を列挙する
        - 部分集合の列挙をビット演算でやる、よく使う方法
    - 2進数の文字列化をして、0と1をAとBに置き換える
- AC
python

```
def main():
    N = int(input())
    group = []
    for i in range(N):
        P = 2 ** (2 ** i)
        group = [x * (P + 1) for x in group]
        group.append(P - 1)

    K = 2 ** N - 1
    print(K)
    for i in range(1, K + 1):
        x = 0
        for j in range(N):
            if (1 << j) & i:
                x = x ^ group[j]
        s = f"{x:0256b}"[-(2 ** N):]
        s = s.replace("0", "A").replace("1", "B")
        print(s)
```

- [アダマール行列 - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%80%E3%83%9E%E3%83%BC%E3%83%AB%E8%A1%8C%E5%88%97)
    - なるほど
    - ${\displaystyle {\boldsymbol {H}}^{\intercal }{\boldsymbol {H}}=n{\boldsymbol {I}}_{n}}$ ということはつまり、$i \neq j$ について $\sum_k H_{ik}H_{kj} = 0$ということ
        - なので、問題条件の「同じチームだった回数が任意のi<jについて等しい」を満たすわけだ
    - 再帰的な構築 $\begin{bmatrix} H & H\\ H & -H\end{bmatrix}$ は気づかなかった
    - 僕がやったのは 群の準同型${\displaystyle \{1,-1,\times \}\mapsto \{0,1,\oplus \}}$ をして ${\displaystyle {\boldsymbol {F}}_{n}={\begin{bmatrix}0_{1\times 2^{n-1}}&1_{1\times 2^{n-1}}\\{\boldsymbol {F}}_{n-1}&{\boldsymbol {F}}_{n-1}\end{bmatrix}}}$することに相当する
        - $0_{1\times 2^{n-1}} 1_{1\times 2^{n-1}}$が P - 1
        - ${\boldsymbol {F}}_{n-1} {\boldsymbol {F}}_{n-1}$が `group = [x * (P + 1) for x in group]`
    - 僕はその後、部分集合ごとにXORしたけど、${\displaystyle {\boldsymbol {H}}_{2^{n}}={\boldsymbol {F}}_{n}^{\intercal }{\boldsymbol {F}}_{n}}$でも良いらしい
        - Fはn行2^n列、各列は異なっているので、nビットの整数が全通り出てくる
            - 順序には意味はない
        - $H_{ij} = \sum_k F_{ki}F_{kj}$なので、これは要するにpopcount(i & j) mod 2
            - 下記のpopcountを使った構築に帰着する
- 公式解説
    - popcount(i & j)を使って構築してる
    - これはアダマール行列の再帰的な構築において、i & jの最上位ビットが1である場合だけ符号反転してるから
        - ![image](https://gyazo.com/5c9aa6ca4a24a6d8af633a07ebb33cf5/thumb/1000)
    - popcount(i & j)がij要素を符号反転した回数になる
