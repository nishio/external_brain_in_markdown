
![image](https://gyazo.com/e061127462d65fbc91305c7902b100a7/thumb/1000)
[N - ビルの建設](https://atcoder.jp/contests/past202004-open/tasks/past202004_n)

from [[第二回 アルゴリズム実技検定]]
PAST2N
- 考えたこと
    - ある点について50000件の正方形の中からそれを含むものを見つけてコストを加算する
    - ただし線形オーダーでは間に合わない
    - どうするか
    - 1次元だったら累積和の変動ポイントを記録しといて二分探索なのだが、今回は二次元だ
    - 2次元いもす法かな？
        - 座標圧縮しても10^5なので二次元でやるのは無理っぽい
- 公式解説
    - [[平面走査法]]
- 改めて考えたこと
    - [[長方形区間add]]
    - これは[[クエリの先読み]]が必要かな
    - クエリごとにN件の正方形の処理をしたら個別の処理がどんなに速くても間に合わない
    - 区間の境界線も含むので混ぜて(y, x)でソート
    - ![image](https://gyazo.com/2fd0b0bd0c92f206061c4b4ef25c4fec/thumb/1000)
- 実装
    - セグメント木を作ろうとして気づいた
        - 値の範囲が10^9→[[座標圧縮]]必要
    - [[RangeAddは二つのPointAdd]]
    - RangeAddとReadが同じ座標で重なった時「正方形の角も正方形の内側」という仕様なので、開始のRangeAddはReadより先に処理されなければならない。
        - 逆に終了のRangeAddは後に処理されなければならない
        - 座標を0.5ずらそう
    - サンプル1は通ったのにサンプル2で負の値が出てきた
        - →座標圧縮したのにセグメント木に元の座標でアクセスしてたミス
- AC
python

```
def solve(N, Q, SS, QS):
    xs = []
    for x, _, width, _ in SS:
        xs.append(x)
        xs.append(x + width)
    for x, _ in QS:
        xs.append(x)
    xs.sort()
    x2i = {}
    for i, x in enumerate(xs):
        x2i[x] = i
    i2x = xs

    commands = []
    for x, y, width, cost in SS:
        start = x2i[x]
        end = x2i[x + width]
        commands.append((
            y, start - 0.5,
            "add",
            start, end, cost
        ))
        commands.append((
            y + width, end + 0.5,
            "add",
            start, end, -cost
        ))
    for x, y in QS:
        commands.append((
            y, x2i[x],
            "read",
            None, None, None
        ))
    commands.sort()
    result = {}

    # segtree
    from operator import add
    set_width(len(x2i) + 10)
    table = [0] * SEGTREE_SIZE
    for y, x, typ, start, end, cost in commands:
        if typ == "add":
            # range add as two point_add
            point_set(table, start, get_value(table, start) + cost, add)
            point_set(table, end + 1, get_value(table, end + 1) - cost, add)
        else:
            # point read as range sum
            v = range_reduce(table, 0, x + 1, add, 0)
            result[(i2x[x], y)] = v

    # print answer
    for q in QS:
        print(result[q])
```


