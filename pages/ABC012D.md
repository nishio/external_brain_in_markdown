
[D - バスと避けられない運命](https://atcoder.jp/contests/abc012/tasks/abc012_4)
- ![image](https://gyazo.com/ee05f83557e61f16cca327eded5de119/thumb/1000)
- 考えたこと
    - 最も遠い頂点までの距離が最小になる点を選んだ時の、その距離を求める問題だと
    - [[グラフの半径]]だね
        - 全方位木DPで求めるんだったかな
            - そんな難しいことをこの難易度で聞かれるかな
            - あっ、これ木じゃないぞ？
    - [[ワーシャルフロイド法]]でO(V^3)か
        - Vは300なので間に合う？
- 公式解説
    - [[ダイクストラ法]]O(V^2)をV回やるかワーシャルフロイド
    - 「ただしPythonなどの遅い言語では通らないことが検証済み」(ええー)
    - ダイクストラをO((E+V)log V)でやる案
        - これ試してみよう
    - PythonでもあっさりACしました
        - 5秒制限のところ1.4秒
        - 6年前の問題だからジャッジマシンが早くなったのかな？
        - それとも「通らないことが検証済み」ってのはV^3の解法のことかな
python

```
def solve(N, M, edges):
    INF = 9223372036854775807
    ret = INF

    for start in range(N):
        distances = [INF] * N
        distances[start] = 0
        queue = [(0, start)]
        while queue:
            d, frm = heappop(queue)
            if distances[frm] < d:
                # already know shorter path
                continue
            for to in edges[frm]:
                new_cost = distances[frm] + edges[frm][to]
                if distances[to] > new_cost:
                    # found shorter path
                    distances[to] = new_cost
                    heappush(queue, (distances[to], to))
        ret = min(ret, max(distances))
    return ret
```


