
from [[動的計画法]]
DP_F
- [[最長部分文字列]]　[[LCS]]
- 0で埋めた二次元配列を作るところをnp.zerosでやったが、生PythonだとTLEなので生リストにしてからPyPyした
- chrはbuffer.readした時に文字が整数値になるので文字列に戻すためにやっている
python

```
def solve(S, T):
    sizeS = len(S)
    sizeT = len(T)
    m = [[0] * (sizeT + 1) for _i in range(sizeS + 1)]
    for i in range(1, sizeS + 1):
        for j in range(1, sizeT + 1):
            m[i][j] = max(
                m[i - 1][j],
                m[i][j - 1],
                m[i - 1][j - 1] + 1 if S[i - 1] == T[j - 1] else 0
            )
    result = []
    i = sizeS
    j = sizeT
    while i > 0 and j > 0:
        if m[i][j] == m[i - 1][j]:
            i -= 1
        elif m[i][j] == m[i][j - 1]:
            j -= 1
        else:
            result.append(chr(S[i - 1]))
            i -= 1
            j -= 1
    print("".join(reversed(result)))
```

