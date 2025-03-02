---
title: "ABC177C"
---

![image](https://gyazo.com/9aee3cdd36ebd15ec417f0041d2af303/thumb/1000)

from [[ABC177]]
ABC177C
[C - Sum of product of pairs](https://atcoder.jp/contests/abc177/tasks/abc177_c)
![image](https://gyazo.com/03b7a549020d2bc77a093d63cb5692b4/thumb/1000)
- 全部出して二乗したものから、対角線を引いて、半分にする
- ![image](https://gyazo.com/9aee3cdd36ebd15ec417f0041d2af303/thumb/1000)
- 求める値をSとすれば$2 S + \sum A_i^2 = (\sum A_i)^2$　#分配法則 [[行列の半分]] [[積と和の交換]]
- 「2で割る」を素朴に割り算切り捨てしててWA
    - 奇数の場合にはMODを足して偶数にしてから2で割る
python

```
def solve(N, AS):
    sum = 0
    sumSq = 0
    for i in range(N):
        sum += AS[i]
        sum %= MOD
        sumSq += AS[i] * AS[i]
        sumSq %= MOD

    ret = (sum * sum - sumSq) % MOD
    if ret % 2 == 0:
        return ret // 2
    else:
        return (ret + MOD) // 2
```

- 公式解説は[[累積和]]だね、横一列を1回の掛け算で済ます方法
    - 僕の解法は「単純に2で割れないから逆元を使った難しい解法になる」と言われてた
        - 抽象的に考えすぎて難しいだけでは。
    - 11ぐらいの小さい数で試したことがあれば難しくなく思いつけると思う
python

```
xs = [None] * 11
for i in range(11):
    xs[i * 2 % 11] = i
# xs => [0, 6, 1, 7, 2, 8, 3, 9, 4, 10, 5]
```

    - こんな感じで2i番目にiが入ってる
    - 奇数番目には一旦最後まで行ってから2周目に値が入る
- ![image](https://gyazo.com/b6ff3cebe067c26861dc9c4c51958d66/thumb/1000)
    - うーん、最速には4ms及ばなかったか！
    - 最速コードは剰余を最後にしか取らない
        - 最大10^30程度なら長整数で押し切った方が速いのかー
        - [[長整数が速い]]
