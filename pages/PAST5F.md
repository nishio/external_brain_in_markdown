---
title: "PAST5F"
---

[F - 一触即発](https://atcoder.jp/contests/past202012-open/tasks/past202012_f)
![image](https://gyazo.com/82689f73ea9cacb95a4584a9b4618956/thumb/1000)

- 2 ** 14 == 16384
- 14 * 13 * 12 == 364
- これは全探索して良いサイズ
    - 14個の薬品を選ぶすべての方法について、最大364個のすべてのルールを確認して「爆発してないから」「一触即発なら、何が危険な薬品か」をチェックする
- 問題条件を勘違いしてWA
    - 一触即発状態での「既に混ぜた薬品の数」ではない
    - 「一触即発状態のルールの数」でもない
    - 「一触即発状態のルールの、まだ追加してない薬品」の集合のサイズが答え
python

```
def solve(N, rules):
    ret = 0
    for subset in range(2 ** N):
        danger = []
        for rs in rules:
            hit = 0
            for r in rs:
                if subset & (1 << (r - 1)):
                    hit += 1
                else:
                    d = r
            if hit == 3:
                danger = []
                break
            if hit == 2:
                danger.append(d)

        ret = max(ret, len(set(danger)))

    return ret
```


