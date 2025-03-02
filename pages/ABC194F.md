---
title: "ABC194F"
---

from [[ABC194]]

[F - Digits Paradise in Hexadecimal](https://atcoder.jp/contests/abc194/tasks/abc194_f)
![image](https://gyazo.com/1a17a7ce598564aed0e289ec0fd8e3cf/thumb/1000)
- 考えたこと
    - [[桁DP]]
    - [[DP S]]をコピペして書き換えた
    - サンプルは通ったんだけど遅い、TLEが解消しない
    - 「16通りの数字が既に出てるかどうかを記録」で6万~になり2×10^5回更新するから厳しいよな
- 公式解説
    - 僕は「何が既に出てるかわからないと、たとえば次に1が出た時に、出現済みの数字の個数が増えるのかどうかわからない」と考えた
    - それは真
    - だけど0〜Fの16通りを計算するのだから、どれが出現済みかわからなくても「16個のうちでいくつで出現済み個数が増えるか」はわかる
    - よって出現済みの数字の個数だけを保持すれば良い
- コンテスト後AC
py

```
def solve(N, K):
    MOD = 1_000_000_007
    D = 16 + 1
    less = [0] * D
    equal_used = [0] * 16
    equal = 0
    for digit in N:
        digit = int(digit, 16)
        new_less = [0] * D
        for d in range(D):
            new_less[d] += less[d] * d

            if d == 0:
                new_less[d] += less[d] * 1
                new_less[d + 1] += less[d] * 15
            elif d != 16:
                new_less[d + 1] += less[d] * (16 - d)

        for new_digit in range(16):
            if new_digit < digit:
                new_d = equal
                if equal_used[new_digit] == 0:
                    new_d += 1
                if new_digit == 0 and equal == 0:
                    new_d = 0
                new_less[new_d] += 1

        for d in range(D):
            new_less[d] %= MOD
        less = new_less
        if equal_used[digit] == 0:
            equal += 1
            equal_used[digit] = 1
    ret = less[K]
    if equal == K:
        ret += 1
    return ret % MOD
```

