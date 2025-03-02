---
title: "ABC184E"
---

![image](https://gyazo.com/3b62a4951b2100ef564ece4d0770989b/thumb/1000)
- [E - Third Avenue](https://atcoder.jp/contests/abc184/tasks/abc184_e)

from [[ABC184]]

- 距離を1ずつ増やしながら幅優先探索
- 必要な値を使いやすい形で読み込むところが泥臭い
    - スタートとゴールは地図に書かずに別途渡して欲しかった
    - [[地図を1次元配列に入れる]]ライブラリをゴリゴリ書き換えることになった
    - そこは特に面白いことはない
- 幅優先探索でTLEしたのでワープの部分が良くないと思いこんでジタバタして4回もTLEしてしまった
    - 同一文字のワープは1回しか使わないことは把握してて、2回試そうとしないように工夫してたのだが、その工夫が足りないのかと思ってしまった
    - 結局原因はそこではなく「次に訪問する頂点」をリストで持ってるところだった
        - 集合に変えたらAC
        - [[AtCoder失敗リスト]]に書いとこう
python

```
def solve(data):
    to_visit = [START]
    DIR4 = dir4()
    ret = 0
    
    while to_visit:
        new_visit = []
        for p in to_visit:
            if p == GOAL:
                return ret

            v = data[p]
            data[p] = -1
            if v > 0:  # WARP
                for p2 in WARP[v]:
                    data[p2] = 0
                    new_visit.append(p2)
                WARP[v] = []
            for d in DIR4:
                p2 = p + d
                if data[p2] >= 0:
                    new_visit.append(p2)
        to_visit = set(new_visit)
        ret += 1
    return -1
```

