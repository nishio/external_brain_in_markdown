
from [[第三回 アルゴリズム実技検定]]
PAST3K
- 複数の机の上に複数の数値の書かれた箱があって、命令に従ってあっちこっち動かす問題。
- 机も箱も20万個あって、命令も20万個ある。
    - ひとつの命令の実行が十分軽くないと時間オーバーする。
- Pythonのリストを配列的に使って、データ構造の意味のリストを作る。 [[リンクトリスト]]
    - これは普通にオブジェクトと参照でやった場合にオーバーヘッドで時間切れになるのを恐れたのと、コードの見た目の違いであって本質的には変わらないよなと思ったから。
    - 長さN+1の配列を4つ用意して、それぞれ「箱iの下の箱」「箱iの上の箱」「机iの一番下の箱」「机iの一番上の箱」を意味している。
    - N+1するのは問題条件が1オリジンだから。
        - 間違えずに1ずらして入出力するより、気にせず使える状況を作った。
        - 0をnullの意味に使えるしね。
        - 問題Eではそれをやらなかったので4箇所でずらしが必要になってる。
- デバッグのためにわかりやすい表示をする関数を用意してあとは素朴に実装する。

python

```
N, Q = [int(x) for x in input().split()]

prev = [-table for table in range(N + 1)]
next = [0] * (N + 1)
top = [table for table in range(N + 1)]
bottom = [table for table in range(N + 1)]


def debugPrint():
    blocks = [[] for i in range(N + 1)]
    for table in range(1, N + 1):
        cur = bottom[table]
        while cur:
            blocks[table].append(cur)
            cur = next[cur]

    print(blocks[1:])


for table in range(Q):
    frm, to, x = [int(x) for x in input().split()]
    # print(frm, to, x)

    p = prev[x]
    if p > 0:
        next[p] = 0
        if top[to]:
            prev[x] = top[to]
            next[top[to]] = x
        else:
            # x is first block of TO
            prev[x] = -to
            bottom[to] = x

        top[to] = top[frm]
        top[frm] = p
    else:
        # x is last block
        bottom[frm] = 0
        if top[to]:
            prev[x] = top[to]
            next[top[to]] = x
        else:
            # x is first block of TO
            bottom[to] = x
            top[to] = top[frm]
            prev[x] = -to

        top[to] = top[frm]
        top[frm] = 0

    # print(prev)
    # print(next)
    # print(top)
    # print(bottom)
    # debugPrint()
    # print()


pos = [0] * (N + 1)
for table in range(1, N + 1):
    cur = bottom[table]
    while cur:
        pos[cur] = table
        cur = next[cur]

for i in range(1, N + 1):
    print(pos[i])
```


他の人のコードを読むと、ここは双方向のリストにする必要はなく、机のトップと、箱の下の箱だけのリストでよいようだ
- [https://atcoder.jp/contests/past202005-open/submissions/14109675](https://atcoder.jp/contests/past202005-open/submissions/14109675)
