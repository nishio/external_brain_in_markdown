
from [[第二回 アルゴリズム実技検定]]
PAST2K
- 考えたこと
    - 変更と削除を行うことで対応の取れた括弧にする問題
    - 文字ごとに変換コストと削除コストが決まっている
    - N=3000
    - 変換してから削除することにメリットはないので「何もしない、変換する、削除する」の三択
    - 括弧をプラマイ1、削除を0とすれば「X番目までの和」をYとしてDPができそう
        - 対応した括弧は、途中で負にならず、最後で0になる
        - 値の範囲は0〜N
        - N^2なので間に合う
- AC
python

```
def solve(N, S, CS, DS):
    INF = 9223372036854775807
    table = [INF] * (N + 1)  # table[N] is sentinel
    table[0] = 0
    for i in range(N):
        new_table = [INF] * (N + 1)
        if S[i] == "(":
            d = 1
        else:
            d = -1

        for j in range(N):
            new_table[j] = min(
                table[j - d],  # no change
                table[j + d] + CS[i],  # change
                table[j] + DS[i],  # delete
            )
        table = new_table
    return table[0]
```


- [[括弧列は上り下り]]
- [[動的計画法]]
- [[範囲上下に番兵]]
