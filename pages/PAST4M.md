
![image](https://gyazo.com/3a479f29390ab0ae87d7f2087d5d94d4/thumb/1000)
from [[第四回 アルゴリズム実技検定]]
[M - 筆塗り](https://atcoder.jp/contests/past202010-open/tasks/past202010_m)
- 考えたこと
    - 実際に塗るのではなく、最も新しい影響するクエリを見つける問題？
    - クエリは10^5、頂点は10^5
    - どうやって見つけるのか
- 公式解説
    - [[時間軸反転]]　[[操作を逆順で考える]]
    - [[塗りの時間軸反転]]
    - [[木の上のパスはLCAで分割できる]]
- 改めて考えたこと
    - 塗りの情報をどうやって保持するか？
    - 各頂点ごとに色を持つのでいいか
    - 1回のクエリで塗られる個数は、高さが平均logNだから対数オーダーだが、当然偏った木で最悪線形オーダーにするテストケースがあるだろう
    - 時間軸を反転することで、一度塗ったところを再度塗らないでスキップしたい
    - それができるためには？
        - 塗りの下端の頂点が「既に塗られてる上端」を持てば良い
    - なっている最中に「既に塗られている頂点」に出逢ったら、塗られてる上端を取得する
        - 塗られてる上端が、今塗ろうとしてる範囲の上端より上なら、そこで終了
        - 下なら塗られてる上端の親から塗りを再開
    - 塗られてる上端を持つのは下端だけではダメ
        - 次のクエリが塗られてる範囲の途中から始まるかもしれないから
    - 上端はどうやってわかる？
        - 塗ろうとしてる上端を見て、それが塗られてるならその上端を得れば良い
    - 自然言語ではこんな感じでできそうな雰囲気だから、後はコードできちんと示す
- 実装
    - [[頂点を塗るのか辺を塗るのか]]
        - 頂点だと勘違いしてたけど辺だな
        - [[木の辺は根以外の頂点と対応する]]
    - 与えられた辺の順序で答えるべきところを、頂点の順序で答えていた

AC:
python

```
def solve(N, Q, edges, QS, ordered_edges):
    from collections import defaultdict
    color = [0] * N
    uplink = [None] * N
    root = 0
    # graph to tree
    children, parents = graph_to_tree(N, edges, root)
    # ready lca
    construct(N, children, root, parents)

    def paint(start, end, c):
        cur = start
        while cur != end:
            if color[cur] == 0:
                color[cur] = c
                uplink[cur] = end
                cur = parents[cur]
            else:
                if query(uplink[cur], end) != end:
                    # uplink if avobe end
                    return
                cur = uplink[cur]

    for a, b, c in reversed(QS):
        a -= 1
        b -= 1
        lca = query(a, b)
        paint(a, lca, c)
        paint(b, lca, c)

    for frm, to in ordered_edges:
        if parents[frm] == to:
            print(color[frm])
        else:
            print(color[to])
```


頂点と辺の取り違え関連でこういうミスをしていた
- uplinkで「過去に塗られた時のend」までジャンプした後、さらにparentに進んでる
    - 頂点ぬりなら正しいのだが、辺ぬりなので正しくない
    - ![image](https://gyazo.com/c4a6f4511b8fe6c3a1fb93a59a34d4eb/thumb/1000)

python

```
def paint(start, end, c):
    cur = start
    while cur != end:
        if color[cur] == 0:
            color[cur] = c
            uplink[cur] = end
        else:
            if query(uplink[cur], end) != end:
                # uplink if avobe end
                return
            cur = uplink[cur]
            if cur == end: return
        cur = parents[cur]
```

