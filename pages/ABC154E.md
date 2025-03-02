---
title: "ABC154E"
---

[E - Almost Everywhere Zero](https://atcoder.jp/contests/abc154/tasks/abc154_e)
![image](https://gyazo.com/3144c591c48ca98ba526eb541f2ade6d/thumb/1000)
- 考えたこと
    - [[桁DP]]ですよね？
        - 100桁についてゼロでない数値の出現回数3のテーブルでDP
        - [[ABC154E_old]]に以前解きかけた残骸のメモがあるな…
        - [[DP S]]を参考にライブラリ化できないかな
    - 桁DPとは
        - 巨大な整数Nが与えられてN以下の非負の整数から条件を満たすものの数を数え上げる時に使える動的計画法アルゴリズム
        - 上位i桁について既知の時にそれを使ってi+1桁の場合を求める
        - 今回の場合なら上位i桁でゼロでない数字をk個つかう場合の和がxなら、0を末尾につけたらkのままi+1桁になる、1〜9ならk+1になる
        - ただし上位i桁がNと一致してる場合だけは例外で、1〜9ではNを超える可能性があるのでNのi+1桁目の値をケアする必要がある
python

```
def solve(N, K):
    less = [0] * (K + 2)
    equal = 0
    for v in N:
        new_less = [0] * (K + 2)
        if v != 0 and equal <= K:
            new_less[equal] += 1  # for 0
            new_less[equal + 1] += v - 1  # for 1..
            equal += 1

        for k in range(K + 1):
            new_less[k] += less[k]  # for 0
            new_less[k + 1] += 9 * less[k]  # for 1..9
        less = new_less

    ret = less[K]
    if equal == K:
        ret += 1
    return ret
```

- AC
