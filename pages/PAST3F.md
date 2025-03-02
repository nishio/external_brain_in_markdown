
from [[第三回 アルゴリズム実技検定]]
PAST3F
F 与えられた文字候補から[[回文]]を作れるかどうか判定して作れるなら一つ出力する問題。「前からN文字目と後ろからN文字目のペア」は他のNと独立しているので分けて考えれば良い。候補の共通部分集合が空集合なら解なし。あれば適当に一つ選べば良い。長さが偶数が奇数かで最後の処理を分ける必要がある。
python

```
N = int(input())
M = []
for i in range(N):
    M.append(input())

answer = []
for i in range(N // 2):
    ok_chars = set(M[i]).intersection(M[N - 1 - i])
    if not ok_chars:
        print(-1)
        break
    answer.append(list(ok_chars)[0])
else:
    if N % 2 == 0:
        print("".join(answer) + "".join(reversed(answer)))
    else:
        print("".join(answer) + M[N//2][0] + "".join(reversed(answer)))
```

