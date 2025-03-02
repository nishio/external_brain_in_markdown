
[K - 巨大企業](https://atcoder.jp/contests/past201912-open/tasks/past201912_k)
- ![image](https://gyazo.com/735b48c1d33a9397fd177016e9fd6b8a/thumb/1000)
- 考えたこと
    - 巨大な木が与えられてaがbの子孫かを判定する問題
    - 素朴にやるとO(NQ)
        - バランスした木なら対数オーダーだから問題ないのだが、すごく偏ってる時に問題
    - 計算結果をキャッシュしたいが、素朴にキャッシュすると空間がN^2になるのでダメ
    - 枝分かれのないパスをキャッシュ？
        - ダメ、二股の分岐がN/2個続くグラフがある
        - 思考の分岐A
    - 偏ってるときだけキャッシュすれば良い？
        - 前処理で一定以上に深い点だけキャッシュ
        - ダメ、N/2より深い頂点をN/2個作れる
    - 思考の分岐A
        - キャッシュ済みの経路に後から合流したことの判定を低コストにできれば良い
        - 例えばある頂点から根までをたどる
        - この時、キャッシュ用の配列Aiにたどった頂点をインクリメントしながら記録
        - 別途キャッシュを見つけるための配列Bにキャッシュ番号iを書き込んでいく
        - 2回目以降、親を辿る際にBを見れば定数オーダーで既にキャッシュされてるかどうかわかる
        - 既にキャッシュされてるならそのキャッシュの目的頂点の番号を見て今の頂点の番号との大小関係を見れば祖先にいるかどうか反対できる
        - キャッシュに見つからなくて素朴に親をたどっていくプロセスは最大N回しか起こらない
        - キャッシュにヒットした後は定数オーダー
        - 追記: この方法は細かいキャッシュをたくさん作られるような入力の時に空間計算量が大きくなるからダメ
    - 公式解説
        - [[最小共通祖先]]lcaが対数オーダーで求められる
            - lca(x, y) = x ならyはxの子孫
            - ダブリングによる最小共通祖先の求めかたの一部で実現できる
                - まず各頂点の深さを求める、これは線形オーダー
                - 2^k個先の親を求める、k一つにつき線形オーダーで、kの値は対数オーダー
                - 与えられた2頂点のうち、深い方の親をたどって深さを揃える
                - この後最小共通祖先を求めるためには二分探索が必要だが、今回は浅い方の頂点が最小共通祖先であるかどうかの判定だけで良い
        - 別解
            - 行きがけ順で頂点を並べる
            - ある頂点の子孫の頂点は、その頂点を始点とする区間に含まれる
            - 行きがけ順での頂点の位置pos(x)と、区間終点の位置end(x)を配列で持っておけば pos(x) < pos(y) <= end(x) ならyはxの子孫
            - 定数オーダー
- AC
    - 0オリジンに変える
    - 各頂点から親へのポインタが渡されているところを、親から子へのポインタに付け替える
    - 各頂点の深さをDFSで求める
    - ダブリングで2^i個上の頂点を求める
    - 各クエリに対して深さの差dを求め、aからdだけ上の頂点がbに一致するか判定する
python

```
def solve(N, PS, Q, QS):
    # PAST1K

    # to 0-origin
    PS = [p - 1 for p in PS]
    from collections import defaultdict
    children = defaultdict(list)
    for i, p in enumerate(PS):
        children[p].append(i)

    # calc depth
    depth = [0] * N

    def visit(v):
        d = depth[v] + 1
        for c in children[v]:
            depth[c] = d
            visit(c)

    root = children[-2][0]
    visit(root)

    # doubling
    parents = [PS]
    for _i in range(20):
        prev = parents[-1]
        next = [0] * N
        for i in range(N):
            next[i] = prev[prev[i]]
        parents.append(next)

    for a, b in QS:
        a -= 1
        b -= 1
        d = depth[a] - depth[b]
        if d < 0:
            print("No")
            continue
        # find d-th parent of a
        p = a
        for i in range(20):
            if d % 2:
                p = parents[i][p]
            d //= 2

        if p == b:
            print("Yes")
        else:
            print("No")
```


[[PAST1]]
