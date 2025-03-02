
[G - ヘビ](https://atcoder.jp/contests/past202012-open/tasks/past202012_g)
![image](https://gyazo.com/3790c397c786b793094fb8a7167295bd/thumb/1000)
- マス目を頂点とし、隣接してるマス目は辺で結んだグラフを考える
    - 頂点は高々16個と小さい
- グラフの各頂点を始点として「すべての頂点を通るパス」をDFS
    - これの計算量を理論的に見積もれてないけど、小さいからいけるだろう的判断
- 与えられたマス目が1個の時、グラフに辺が0本になる。これがコーナーケースでWAした
    - `(1)`で手当てした
    - が、これはそもそも頂点のリストを作ってないところに問題がある
    - 「辺が双方向だから辺の始点の集合が頂点の集合だろう」→間違い、辺がないケースがある
- 地図は[[地図読み込み時に番兵をつける]]で読んでる
    - 隣接関係でグラフにするところはライブラリ化してもいいかもな
python

```
def solve(H, W, data):
    from collections import defaultdict
    # make graph
    edges = defaultdict(list)
    count = 0
    a_vertex = None
    for x in range(H):
        for y in range(W):
            v = W * x + y
            pos = WIDTH + 1 + WIDTH * x + y
            if data[pos]:
                a_vertex = v
                count += 1
                if data[pos + 1]:
                    edges[v].append(v + 1)
                    edges[v + 1].append(v)
                if data[pos + WIDTH]:
                    edges[v].append(v + W)
                    edges[v + W].append(v)

    if count == 1:  # (1)
        print(1)
        v = a_vertex
        x, y = divmod(v, W)
        print(x + 1, y + 1)

    for start in edges:
        visited = [False] * (H * W)
        path = []

        def visit(cur):
            visited[cur] = True
            path.append(cur)
            if len(path) == count:
                return True
            for next in edges[cur]:
                if not visited[next]:
                    r = visit(next)
                    if r:
                        return True
            visited[cur] = False
            path.pop()

        if visit(start):
            print(count)
            for v in path:
                x, y = divmod(v, W)
                print(x + 1, y + 1)
            return
```


