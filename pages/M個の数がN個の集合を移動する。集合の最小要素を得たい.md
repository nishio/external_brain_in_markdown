
from [[heapq]]
集合がN個あり相異なるM個の数が集合から集合へ移動する。ある集合の最も小さい数を得たい。
→「今どの集合にあるか」をサイズMの配列で別途保存。集合から離れる時にheapqから削除しない。追加も移動も同じコード。取得の時にその集合にいない要素を読み飛ばす。
python

```
N = 2
M = 2
items = [[] for _ in range(N)]
position = [-1] * M


def put(id, pos):
    heappush(items[pos], id)
    position[id] = pos


move = put


def top(pos):
    q = items[pos]
    while q:
        id = q[0]
        if position[id] != pos:
            heappop(q)
            continue
        return id
    return None


put(0, 0)
put(1, 0)

move(0, 1)
print(top(0))  # => 1
move(0, 0)
print(top(0))  # => 0
move(0, 1)
print(top(0))  # => 1
```

