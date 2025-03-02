---
title: "PAST2H"
---

![image](https://gyazo.com/d8cd95f94d454f735f18cfccd5356534/thumb/1000)
[H - 1-9 Grid](https://atcoder.jp/contests/past202004-open/tasks/past202004_h)

from [[第二回 アルゴリズム実技検定]]

- 考えたこと
    - 同じマスを何度も通って良いことが厄介、到達不可能な時に無限ループにハマらないようにしたい
    - 二次元ではなく0〜9のフロアがあると考える
        - フロアiから1歩動いて、移動先がi+1である時に限りフロアを登る階段がある
        - フロア0のSからフロア9のGまでの最短経路問題
    - 公式解説と違う
- 時間を置いて考えたこと
    - [[ダイクストラ法]]で解くので辺にコストがついてていいから「フロアiから1歩動いて、移動先がi+1である時に限りフロアを登る階段がある」ではなく「フロアiの数値iは下のフロアから上に上がるコスト0の辺がある」にした
    - グラフを構築したらダイクストラ法で最短距離を求めるだけ
- AC
python

```
def solve(HEIGHT, WIDTH, data):
    from collections import defaultdict
    edges = defaultdict(dict)
    W = WIDTH
    H = HEIGHT
    for level in range(10):
        for y in range(HEIGHT):
            for x in range(WIDTH):
                pos = x + y * WIDTH + level * WIDTH * HEIGHT
                v = data[y][x]
                if x < W - 1:
                    edges[pos + 1][pos] = 1
                if x > 0:
                    edges[pos - 1][pos] = 1
                if y < H - 1:
                    edges[pos + W][pos] = 1
                if y > 0:
                    edges[pos - W][pos] = 1
                if v == "S":
                    if level == 0:
                        start = pos
                elif v == "G":
                    if level == 9:
                        goal = pos
                else:
                    v = int(v)
                    if v == level:
                        edges[pos - W * H][pos] = 0

    return one_to_one(start, goal, 10 * W * H, edges)
```

- 公式解説は動的計画法で求めている
    - 計算量的にはダイクストラの方が軽い
