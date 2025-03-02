
[K - Stones](https://atcoder.jp/contests/dp/tasks/dp_k)
- 対戦ゲームの読み切り問題
- 盤面を定義域とするDP
    - 盤面は整数1つで表現できる
    - 「その盤面を渡された人が勝つか負けるか」を値とする
    - 取るものが残ってなくて負ける終盤から逆にたどる
        - [[時間軸反転]]
python

```
def solve(N, K, AS):
    AS.sort()
    MIN = AS[0]
 
    table = [0] * (K + 1)
    for i in range(MIN):
        table[i] = -1  # LOSE
 
    for i in range(MIN, K + 1):
        for a in AS:
            if table[i - a] == -1:
                table[i] = 1
                break
        else:
            table[i] = -1
 
    # debug(": table", table)
 
    if table[K] == 1:
        return "First"
 
    else:
        return "Second"
```

[https://atcoder.jp/contests/dp/submissions/15052948](https://atcoder.jp/contests/dp/submissions/15052948)
