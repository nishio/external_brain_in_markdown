---
title: "ABC179D"
---

![image](https://gyazo.com/7b170df6b0f48886ab9a41790797f20e/thumb/1000)

[D - Leaping Tak](https://atcoder.jp/contests/abc179/tasks/abc179_d)
- ![image](https://gyazo.com/39b5c5d2890f126f81169312eb00f3b3/thumb/1000)
- しばらく悩んで、飛ばしてEへ
    - 悩み「え、これ範囲が広いと困るのでは？」←正しい
- 素朴にメモ化再帰DPで書いてみて案の定[TLE](https://atcoder.jp/contests/abc179/submissions/16881501)
- 小さい方からループで塗りつぶすDPにしても[TLE](https://atcoder.jp/contests/abc179/submissions/16882554)
- でもそのコードを見て「あ、要するにこの最内ループを潰せばいいんだな」と気づく
    - [[累積和]]で[AC](https://atcoder.jp/contests/abc179/submissions/16885434)
- 少し綺麗にしたコード
python

```
def solve(N, K, SS):
    count = [0] * (N + 10)
    count[0] = 1
    accum = [0] * (N + 10)
    accum[0] = 1

    for pos in range(1, N):
        ret = 0
        for left, right in SS:
            start = pos - right - 1
            end = pos - left
            ret += (accum[end] - accum[start])
            ret %= MOD
        count[pos] = ret
        accum[pos] = accum[pos - 1] + ret

    ret = count[N - 1]
    return ret % MOD
```

- Twitter見てたら「[[いもす法]]だ」とか言ってる人がいたけど、そうかな。僕はそういう意識はなかった。
    - DPの計算をする上で範囲の和を計算する部分が、範囲が広い時に「たくさんの数を足し合わせる」になって遅いのが解決すべき問題
    - そこで「今までに計算した数の和」の配列を別途作ってやる
        - これは「新しい値を前の値に足す」で作れる
        - これを[[累積和]]と言ってる
    - いざ広い範囲の和が必要になった時には、範囲終了点での累積和から範囲開始点の一つ手前の累積和を引けば得られる
    - ![image](https://gyazo.com/7b170df6b0f48886ab9a41790797f20e/thumb/1000)
- Twitter見てたら[[セグメント木]]だと言ってる人もいる
    - セグメント木は範囲和がO(logN)なので、ループで回して和を計算するO(N)よりは速くなる
        - 今回使った累積和はO(1)なのでさらに速い
    - 累積和は先頭からしか値を入れられないが、セグメント木では任意の位置に入れられる。この柔軟性の分だけ遅いと言えるだろう。
    - 今回は先頭からDPするので任意位置に入れられる必要はなかった。

[[ABC179]]
