
from [[ABC190]]
ABC190E
[E - Magical Ornament](https://atcoder.jp/contests/abc190/tasks/abc190_e)[E - Magical Ornament](https://atcoder.jp/contests/abc190/tasks/abc190_e)
- ![image](https://gyazo.com/79456a6bfd6230660714426024778981/thumb/1000)
- 辺の数の制約があるので[[辺が10^5ならダイクストラ使える]]を思いつく
- 高々17頂点なので17回ダイクストラしてC頂点間の距離を求めて巡回セールスマン問題(始点に戻らないタイプ)
- サンプルはあっさり通ったが、提出すると20AC 5WA 10TLE
    - 厄介だな…
- WAの原因
    - 到達不能判定をする時にダイクストラの結果にINFが含まれるかで判断してた
    - それは「グラフのいずれかの頂点が到達不能か？」を判定している
    - C頂点が到達可能なら他の頂点はどうでもいい
- TLEの解決方法が皆目検討つかず時間切れ
- 公式解説
    - 17回BFSして[[最短ハミルトン路問題]]
    - え、じゃあダイクストラではなくBFSしてたら通ったということ？
    - 試したら通った…
python

```
def main():
    N, M = map(int, input().split())
    from collections import defaultdict
    edges = defaultdict(list)
    for _i in range(M):
        frm, to = map(int, input().split())
        edges[frm - 1].append(to - 1)  # -1 for 1-origin vertexes
        edges[to - 1].append(frm - 1)  # if bidirectional

    K = int(input())
    CS = list(int(x) - 1 for x in input().split())

    INF = 9223372036854775807
    dist = []
    for c in CS:
        d = one_to_all_bfs(c, N, edges, INF)
        dd = [d[CS[i]] for i in range(K)]
        if INF in dd:
            print(-1)
            return
        dist.append(dd)

    ret = tsp_not_return(K, dist)
    print(ret + 1)
```

    - コード全体はこちら[AC](https://atcoder.jp/contests/abc190/submissions/19822810)
