---
title: "N個の値が更新される、最小値を知りたい"
---

from [[heapq]]
N個の値があり、更新されていく、最小値を知りたい。
→どの値がいつ何に更新されたかのタプルをキューに入れる。サイズNの配列で値の最終更新時刻を保存する。取得時に最新でない情報を読み飛ばす。
python

```
N = 2
values = [None] * N
lastUpdate = [0] * N
queue = []
time = 0


def update(pos, value):
    global time
    time += 1
    values[pos] = value
    heappush(queue, (value, pos, time))
    lastUpdate[pos] = time


def top():
    while queue:
        value, pos, time = queue[0]
        if time == lastUpdate[pos]:
            return value
        heappop(queue)
    return None


update(0, 42)
print(top())  # => 42
update(1, 43)
print(top())  # => 42
update(0, 44)
print(top())  # => 43
```

