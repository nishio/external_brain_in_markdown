
[V - Subtree](https://atcoder.jp/contests/dp/tasks/dp_v)
- 木が与えられる、どの黒頂点から黒頂点へも黒頂点だけを通って到達できるような塗り分けの総数を求める問題
    - 部分木の個数を求めるって理解でいいのかな？
    - あ「頂点vが黒であるような組み合わせは何通りか」を答えるのか。単純に部分木を求めるのではオーダーがN倍になっちゃうから部分問題を使いまわしたいわけね
    - [[全方位木DP]]

- 素朴に作って問題が大きいところだけRE
    - タプルをキーにした辞書が遅かろうと思って積の整数をインデックスにしてた
    - Nが10^5まで行くので2乗で10^10になってMemoryError
        - 手元ではメモリがたくさんあるので動いてしまう
        - MLEではなくREになるので原因がわかりにくかった
    - RE [https://atcoder.jp/contests/dp/submissions/15106317](https://atcoder.jp/contests/dp/submissions/15106317)

- 修正してもTLE [https://atcoder.jp/contests/dp/submissions/15114039](https://atcoder.jp/contests/dp/submissions/15114039)
    - 1つの頂点から生えている辺が多い時に集計がO(N)になってしまう
    - 「たくさんの中から1つ取り除いたものの集計」を演算結果を使い回して計算量削減する必要がある
    - 乗算での集計は0に逆元がないので「全部かけたものから一つだけ戻す」ができない、加算なら逆元があるからできるのだが…。
    - というわけで前からと後ろからの累積積を作る
    - これって位数制限のないグラフだと常に必要になると思う

python

```
N = 700
xs = range(1, N + 1)

head = [0] * (N + 1)
cur = 1
for i in range(N):
    cur *= xs[i]
    head[i] = cur
head[-1] = 1

tail = [0] * (N + 1)
cur = 1
for i in range(N - 1, -1, -1):
    cur *= xs[i]
    tail[i] = cur
tail[-1] = 1

one_out_product = [head[i - 1] * tail[i + 1] for i in range(N)]
# print(head)
# print(tail)
# print(one_out_product)

if not"TEST":
    bluteforce = [1] * N
    for i in range(N):
        for j in range(N):
            if i == j:
                continue
            bluteforce[i] *= xs[j]

    #print(bluteforce)
    assert bluteforce == one_out_product 
```

作ったはいいが、これの実行タイミングは？

他の人のコードを読む
- [https://atcoder.jp/contests/dp/submissions/14624575](https://atcoder.jp/contests/dp/submissions/14624575)
- Python  523msec
- なるほど、僕のコードは「全部白、根が黒い、それ以外で根が白い」の3つにわけて後者二つを伝搬してるけど、子供の根が白いと親が黒になり得ないので最終計算の時に必ず無視されるから伝搬する必要がないのか
    - 「子供の値を掛け合わせて1を足したもの」という更新で良い
    - 1を足すのは子供が全白のパターン
- しかも再帰呼び出しは必要ない、と。最初に幅優先探索でたどった順番を記録している。またその時に逆向きの辺を消している。
- ![image](https://gyazo.com/b910e1af8eb9355d9717ec6f26604f7f/thumb/1000)


python

```
def solve(N, M, edges):
    # convert bidirectional graph to tree
    root = 1
    parent = [-1] * (N + 1)
    to_visit = deque([root])
    bfs_visited_order = []
    while to_visit:
        cur = to_visit.popleft()
        bfs_visited_order.append(cur)
        for child in edges[cur]:
            if child == parent[cur]:
                continue
            parent[child] = cur
            edges[child].remove(cur)  # remove back-link
            to_visit.append(child)

    # up-edge: v -> parent[v]
    # default: if no child, one black, one white (1 + 1)
    # f(x) = prod(f(c) for c in children) + 1
    upedge = [0] * (N + 1)
    # stores multiply result (1 is unity)
    multiply_of_upedge = [1] * (N + 1)
    for cur in reversed(bfs_visited_order[1:]):
        # visit vertexes except root, in reversed order
        upedge[cur] = multiply_of_upedge[cur] + 1
        p = parent[cur]
        multiply_of_upedge[p] *= upedge[cur]
        multiply_of_upedge[p] %= M
    # root: multiply children and don't add one
    # the one is "all-white" pattern
    upedge[root] = multiply_of_upedge[root]
    final_result = upedge[:]

    # down-edge: parent[v] -> v
    downedge = [1] * (N + 1)
    for cur in bfs_visited_order:
        prod = 1
        # left-to-right accumlated products (* downedge[cur])
        for child in edges[cur]:
            downedge[child] = prod
            prod *= upedge[child]
            prod %= M
        # multiply right-to-left accumlated products
        prod = 1
        for child in reversed(edges[cur]):
            downedge[child] = (downedge[cur] * downedge[child] * prod) % M + 1
            prod *= upedge[child]
            prod %= M

        for child in edges[cur]:
            # update final result
            final_result[child] = (
                multiply_of_upedge[child]
                * downedge[child]) % M

    return final_result[1:]
```

[https://atcoder.jp/contests/dp/submissions/15122587](https://atcoder.jp/contests/dp/submissions/15122587)
