
[E - ハンコ](https://atcoder.jp/contests/past202012-open/tasks/past202012_e)
![image](https://gyazo.com/96531e5dba571b147d99cf54cec7253f/thumb/1000)
- 素朴に全探索すれば良い
- はみださないように全探索するために、スタンプでない側にスタンプの幅分の[[番兵]]をつけた
- 番兵をつけるコード自体は既に書いてあった
    - [[地図読み込み時に番兵をつける]]
    - 今まで、一度に二つ読むことはなかったのでグローバル空間に番兵つきの幅を書き込んでいた
    - 今回は二つ読むのでその値を参照しないで再計算するコードになった
        - 改善の余地はあるが、使う頻度低そう…
- 回転は想定してなかったので今回新たに書いた
    - 回転時に縦横の長さが交換される
    - スタンプの側だけを交換するべきだが取り違えててWAした
python

```
def solve(H, W, world, stamp):
    S = max(H, W)
    # world
    WW = W + 2 * S
    WH = H + 2 * S
    # stamp
    SW = W
    SH = H

    def conflict():
        for x in range(SW):
            for y in range(SH):
                if stamp[y * SW + x] == 0:
                    if world[(sy + y) * WW + (sx + x)] == 0:
                        # conflict
                        return True

    for _rot in range(4):
        for sx in range(S + W):
            for sy in range(S + H):
                if conflict():
                    continue
                return True
        # rotate
        new_stamp = [0] * (W * H)
        for x in range(SH):
            for y in range(SW):
                new_stamp[y * SH + x] = stamp[(SH - 1 - x) * SW + y]
        stamp = new_stamp
        SW, SH = SH, SW

    return False
```

- 公式解説
    - スタンプの側を座標の列で持てば回転の実装も素直に書ける、なるほど
    - [[二次元配列を座標の列にする]]
