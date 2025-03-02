---
title: "✅ARC074D"
---

![image](https://gyazo.com/4d90135f13838ae486c33a1424fb914d/thumb/1000)

[F - Lotus Leaves](https://atcoder.jp/contests/arc074/tasks/arc074_d) diff: 2208
![image](https://gyazo.com/a72c294639d6c322d4bc4d623b87f6a0/thumb/1000)
- 考えたこと
    - [[最小カット]]がらみであることは既知
    - グラフが与えられて頂点SからTまで到達できないようにするためにいくつの頂点を取り除けば良いかを答える問題
    - 取り除くのが「頂点」ではなく「辺」なら素直な最小カットの問題
    - ということは[[頂点を辺に変換]]すればいい
    - ![image](https://gyazo.com/9fff8fc0b6b978f7275bebef8db70e1c/thumb/1000)
    - 新しく導入した赤い辺だけを重み1にし、他の辺を重み無限にする。最小カットを求めれば赤い辺を最小の本数切断する。
    - それ以外の辺は切られない程度に太くすれば良い
    - 到達不能にできないのはSとTが並んでる時、それ以外は最悪全ての頂点を取り除けば到達不能にできる

1 MLE
[https://atcoder.jp/contests/arc074/submissions/20593919](https://atcoder.jp/contests/arc074/submissions/20593919)
- ライブラリの実装が悪いか、使い方が悪いか
- 最悪20000頂点、10000頂点から199本の辺がでる
- 行と列の頂点を追加すれば+200頂点で、各頂点から出るのは2本になるが…
- メモリ食いすぎるのはハッシュテーブルがメモリ食いなせいだよな…

AC
- 20万辺は厳しそうだったのと、[[最小カット勉強会]]で試してみて頂点数が増えることの影響はあまり大きくなさそうだったので、頂点数を増やして辺を削減することにした
- 各頂点から「縦または横に並んでる頂点」に直接辺を張るのではなく「縦頂点」「横頂点」を介してつながるようにした
    - [[多対多の関係に仲介者を置く]]
    - ![image](https://gyazo.com/418e454dc8ceb664691dcafdb6fc94a4/thumb/1000)

- これで最悪200万本だったのが3万本まで減る
py

```
def solve(H, W, world):
    CHAR_S, CHAR_T, CHAR_O = b"STo"
    leaf = set()
    for pos in world.allPosition():
        if world.mapdata[pos] == CHAR_S:
            start = pos
        if world.mapdata[pos] == CHAR_T:
            goal = pos
        if world.mapdata[pos] == CHAR_O:
            leaf.add(pos)

    sy, sx = divmod(start, W)
    gy, gx = divmod(goal, W)
    if sy == gy or sx == gx:
        return -1

    INF = 10000
    d = Dinic(H * W * 2 + H + W)
    O_BG = H * W
    O_Y = H * W * 2
    O_X = H * W * 2 + H
    for pos in leaf:
        pos2 = pos + O_BG
        d.add_edge(pos, pos2, 1)
        y, x = divmod(pos, W)
        d.add_edge(pos2, y + O_Y, INF)
        d.add_edge(pos2, x + O_X, INF)
        d.add_edge(y + O_Y, pos, INF)
        d.add_edge(x + O_X, pos, INF)

    d.add_edge(start, sy + O_Y, INF)
    d.add_edge(start, sx + O_X, INF)
    d.add_edge(gy + O_Y, goal, INF)
    d.add_edge(gx + O_X, goal, INF)

    ret = d.max_flow(start, goal)
    return ret
```


