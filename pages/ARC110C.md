
from [[ARC110]]
[C - Exoswap](https://atcoder.jp/contests/arc110/tasks/arc110_c) [[ARC110F]]に関連問題
![image](https://gyazo.com/f71976b9a1f12a846b3cf359703b0135/thumb/1000)

ARC110C
- 貪欲にやる
- 「1を先頭に持ってくるには」を考える
    - 今いる位置から先頭まで持ってくる置換が必要不可欠
- 順番に先頭に持ってくる過程をやって、過不足が有ればNG
- 関連: [[貪欲法の証明パターン]]
python

```
def solve(N, PS):
    ret = []
    used = [False] * (N - 1)

    def swap(x):
        PS[x - 1], PS[x] = PS[x], PS[x - 1]
        used[x - 1] = True
        ret.append(x)

    for target in range(1, N):
        x = PS.index(target, target - 1)
        for i in range(x, target - 1, -1):
            if used[i - 1]:
                return [-1]
            swap(i)

    if False in used:
        return [-1]
    return ret
```

