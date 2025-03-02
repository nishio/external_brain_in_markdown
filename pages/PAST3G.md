---
title: "PAST3G"
---

from [[第三回 アルゴリズム実技検定]]
PAST3G
G
- 障害物のあるグリッドの上を将棋の金将がスタートからゴールまで移動するときの最短経路長を求める問題。
    - [[グリッドグラフ]] [[最短経路問題]]
- 幅優先探索。障害物が置かれうる範囲の外側1マス用意すれば迂回経路には十分。
- バグりやすそうなのでまずグリッドのサイズを5x5にしたバージョンでデバッグ出力しながらバグを潰した。
- 初回提出は訪問済みのマスに印をつけ忘れてタイムリミット超過。小さいデータでテストしてた時は気づかなかった。
- 2回目提出はランタイムエラー、グリッドサイズを1マス少なく計算してた。-1から1の範囲にマス目は3つある。

python

```
TINY_TEST = False

if TINY_TEST:
    MIN_BOUND = -2
    MAX_BOUND = 2
else:
    MIN_BOUND = -200
    MAX_BOUND = 200

WIDTH = (MAX_BOUND - MIN_BOUND) + 4  # why not 3?
M = [["."] * WIDTH for i in range(WIDTH)]


def setMap(p, v):
    x, y = p
    M[y - MIN_BOUND + 1][x - MIN_BOUND + 1] = v


def getMap(p):
    x, y = p
    return M[y - MIN_BOUND + 1][x - MIN_BOUND + 1]


START = (0, 0)
if TINY_TEST:
    GOAL = (2, 2)

    setMap(START, "S")
    setMap(GOAL, "G")
    obstacles = [(1, 1)]
    for p in obstacles:
        setMap(p, "#")
else:
    N, X, Y = [int(x) for x in input().split()]
    setMap((X, Y), "G")
    for i in range(N):
        p = [int(x) for x in input().split()]
        setMap(p, "#")


def pp(map):
    for line in map:
        print("".join(line))


def main():

    def visit(x, y):
        if getMap((x, y)) == "G":
            return True
        if getMap((x, y)) != ".":
            return
        if x < MIN_BOUND-1 or MAX_BOUND+1 < x:
            return
        if y < MIN_BOUND-1 or MAX_BOUND+1 < y:
            return
        newFront.append((x, y))
        setMap((x, y), "v")

    newFront = [START]
    for numSteps in range(1, 1000):
        front = set(newFront)
        # print("len front,", len(front), numSteps)
        # print(front)
        newFront = []
        for x, y in front:
            isFinished = (
                visit(x + 1, y + 1)
                or visit(x, y + 1)
                or visit(x - 1, y + 1)
                or visit(x + 1, y)
                or visit(x - 1, y)
                or visit(x, y - 1))
            if isFinished:
                print(numSteps)
                return
        if not newFront:
            print(-1)
            return


main()
```

