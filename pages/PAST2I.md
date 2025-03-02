---
title: "PAST2I"
---

from [[第二回 アルゴリズム実技検定]]
![image](https://gyazo.com/edc8d1afb55b0c9082e68b8470ffa0e0/thumb/1000)
[I - トーナメント](https://atcoder.jp/contests/past202004-open/tasks/past202004_i)

PAST2I
- 対戦相手のIDが既知なら勝敗は定数オーダーでわかる
- なので一回戦の勝者IDをキューに入れて二回戦ではそれを読めば良い
- 決勝戦を行う必要はないので`while len(winner) > 2`
python

```
def solve(N, AS):
    ranks = [1] * (2 ** N)
    winner = list(range(2 ** N))
    next_rank = 2

    while len(winner) > 2:
        next_winner = []
        for i in range(0, len(winner), 2):
            a = winner[i]
            b = winner[i + 1]
            if AS[a] > AS[b]:
                next_winner.append(a)
                ranks[a] = next_rank
            else:
                next_winner.append(b)
                ranks[b] = next_rank
        winner = next_winner
        next_rank += 1
    return ranks
```


