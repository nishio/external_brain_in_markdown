
from [[第四回 アルゴリズム実技検定]]
PAST4G
[G - 村整備](https://atcoder.jp/contests/past202010-open/tasks/past202010_g)
- 考えたこと
    - 高々100マス
    - 連結成分が1個なら全ての壁
    - 2個ならそれをつなぐ壁
    - 3個以上ならそれをつなぐ壁
    - 4個でもそう
    - 5個以上なら0
    - ライブラリの改善メモ
        - 読んだものをどうエンコードするか指定できるといいな
        - 用意してたライブラリでは壁が0、道が1になるが、今回は色番号で塗りたいので大きめの数にした
        - 4方位、8方位、なども定数にしておく
            - C問題でも使ったので。
    - 補足
        - 隅からDFSで塗っていく
        - まだ塗られていないマスが見つかったら色数をインクリメント
        - 色数が5以上なら0
        - 各マスについて四方の色を確認、すべての色が出現しているマスを数える
python

```
def solve(H, W, data):
    DOT = 100
    BLOCK = 101

    def paint(pos, color):
        data[pos] = color
        for d in [-WIDTH, -1, +1, +WIDTH]:
            if data[pos + d] == DOT:
                paint(pos + d, color)

    color = 0
    for pos in allPosition():
        if data[pos] == DOT:
            paint(pos, color)
            color += 1

    if color >= 5:
        return 0
    ret = 0
    for pos in allPosition():
        if data[pos] != BLOCK:
            continue
        color_exists = [0] * 4
        for d in [-WIDTH, -1, +1, +WIDTH]:
            c = data[pos + d]
            if c < 4:
                color_exists[c] = 1
        if sum(color_exists) == color:
            ret += 1

    return ret
```

- 公式解説
    - マップが10×10とかなり小さい
    - なので、各壁を始点として「その壁を壊したらすべての壁でないマスが到達可能になるか？」を探索しても10^4程度で余裕
        - O(N^4)
    - 僕の解法はO(N^2)なのでオーバーキルであった
