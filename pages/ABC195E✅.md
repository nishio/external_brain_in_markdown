---
title: "ABC195E✅"
---

from [[ABC195]]
ABC195E
- [[ゴールから逆算]]
- 素直に書いて、手元テスト一発で通って、提出もACだったのであんまり書くことが思いつかない
py

```
def main():
    N = int(input())
    SS = input().strip().decode('ascii')
    XS = input().strip().decode('ascii')

    goal = [0] * 7
    goal[0] = 1  # if 1 Taka win

    for i in reversed(range(N)):
        s = int(SS[i])
        prev_goal = []
        if XS[i] == "A":
            for prev in range(7):
                if goal[(prev * 10 + s) % 7] == 0 or goal[(prev * 10) % 7] == 0:
                    prev_goal.append(0)
                else:
                    prev_goal.append(1)
        else:  # "T" 
            for prev in range(7):
                if goal[(prev * 10 + s) % 7] == 1 or goal[(prev * 10) % 7] == 1:
                    prev_goal.append(1)
                else:
                    prev_goal.append(0)
        goal = prev_goal

    if goal[0] == 1:
        print("Takahashi")
    else:
        print("Aoki")
```

- > E問題は、[[AGC045A]]『Xor Battle』の簡単版なのだ！ [tw](https://twitter.com/kyopro_friends/status/1370732280524599296)
