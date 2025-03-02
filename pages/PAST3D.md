---
title: "PAST3D"
---

from [[第三回 アルゴリズム実技検定]]
PAST3D
D　LEDの点灯情報から表示された数値を読み取る問題。認識すべきパターン以外のものが来ないことが保証されてるので、認識すべきパターンのリストを作って完全一致で比較。もちろんこのパターンのリストはプログラムで使ってる。Pythonの対話的コンソールでささっと変形。
python

```
N = int(input())
S = [input(), input(), input(), input(), input()]

PATTERNS = """
####.##.##.####
.#.##..#..#.###
###..#####..###
###..####..####
#.##.####..#..#
####..###..####
####..####.####
###..#..#..#..#
####.#####.####
####.####..####
""".strip().split()

result = ""
for i in range(N):
    char = "".join(S[j][i * 4 + 1:i * 4 + 4] for j in range(5))
    result += str(PATTERNS.index(char))
print(result)
```

