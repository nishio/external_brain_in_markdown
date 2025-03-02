
from [[第四回 アルゴリズム実技検定]]
PAST4D
[D - 分身](https://atcoder.jp/contests/past202010-open/tasks/past202010_d)
- 考えたこと
    - 空欄を端から埋めていく問題
    - 端に接触してる空欄があるならその長さは最低限必要
    - 空欄の個数を数える
    - 補足: 最長の空欄が、両端の空欄を足したものの以下なら、両端の空欄を埋めるように動けばそれで十分埋まる
- 補足
    - [[操作の順序は関係ない]]
- 公式解説
    - 50×50なので全探索しても良い
python

```
def solve(N, S):
    spaces = []
    if S[0] == ord("#"):
        spaces.append(0)
        state = "BLOCK"
    else:
        state = "SPACE"
    c = 0

    for i in range(N):
        if state == "SPACE":
            if S[i] == ord("."):
                c += 1
            else:
                spaces.append(c)
                state = "BLOCK"
        else:
            if S[i] == ord("."):
                state = "SPACE"
                c = 1
            else:
                pass
    if state == "BLOCK":
        spaces.append(0)
    else:
        spaces.append(c)

    m = max(spaces)
    if m > spaces[0] + spaces[-1]:
        print(spaces[0], m - spaces[0])
    else:
        print(spaces[0], spaces[-1])
```

