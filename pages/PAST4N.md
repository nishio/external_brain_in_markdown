---
title: "PAST4N"
---

from [[第四回 アルゴリズム実技検定]]
PAST4N

[N - マス目の穴埋め](https://atcoder.jp/contests/past202010-open/tasks/past202010_n)
![image](https://gyazo.com/68a9ca92e218c196afc3b9fe1065c77f/thumb/1000)

- 考えたこと
    - ?を埋める方法のうち、全て周囲の中央値であるものの個数
    - ?どうしが影響を与えるのがやっかい
    - 全部はてななんてのがある
        - DP?
        - 升目は18行6列
        - 6列のパターンが決まればOKなDP
    - 周り3つが同じ値の時だけNG
    - 6列のパターンだけでなく、上のマスの周囲にいくつ1があるか、が必要？
        - 上が1,0,0で1になってる時、下に0を置いてはいけない
        - 危うい0,1も含めると2ビット必要
    - ダメだ
        - 隣に0を置かれたことで危ない0に後からなることがある
- 公式解説
    - 2列でDP
    - [[小さな定数に注目]]、6ってのは、2倍にしてもbit DPできるということ
    - 持ち回る情報を小さくしすぎた、大きい方から考えた方が良かったか
        - 上の行の情報がすべて得られるなら十分今の行の特定ができる
        - ならばどこまでが必要か？
        - 3つ上は必要ない
        - よって2行でDP
        - …という流れで考えるべきだったか
- 改めて考える
    - 2列の情報を2^12にパックして、1行進むごとに6ビットシフトする
    - 与えられたヒントデータはビットマスクにして矛盾の有無はビット演算でやる
        - 1があるべきところすべてに1があることはマスクをandしてマスクと同一か調べれば良い
        - 0があるべきところに0があるかは逆のマスクをorすれば良い
    - 周囲の中央値であることは素朴に調べるしかないかなぁ
        - 端があるので厄介だし
        - 問題文を読み返したら端は0扱いだった
        - 周囲4つを足した値が2以上なら1が、2以下なら0がvalid、2の時は両方
- 5AC 14WA　とりあえずTLEはしないみたい
    - サンプルも含めると8ACなので根本的に間違ってるということはなさそう
    - 何がおかしいのか…
python

```
def solve(data):
    ZERO = ord("0")
    ONE = ord("1")

    onemasks = []
    zeromasks = []
    for y in range(18):
        onemask = 0
        zeromask = 0
        for i in range(6):
            if data[y][i] == ONE:
                onemask += 1 << i
            if data[y][i] != ZERO:
                zeromask += 1 << i
        onemasks.append(onemask)
        zeromasks.append(zeromask)

    def is_valid(y, s):
        return (
            onemasks[y] & s == onemasks[y] and
            zeromasks[y] | s == zeromasks[y]
        )

    def is_median(p1, p2, s):
        for i in range(6):
            # median check
            mask = (1 << i)
            neighbor = sum(
                x & mask > 0 for x in
                [p1, (p2 << 1), (p2 >> 1), s])
            is_ok_one = (p2 & mask) and neighbor >= 2
            is_ok_zero = not(p2 & mask) and neighbor <= 2
            if not (is_ok_one or is_ok_zero):
                return False
        return True

    def debugprint(*args):
        def to_s(x):
            return "".join(reversed(f"{x:06b}"))
        print(*[to_s(x) for x in args], sep="\n", file=sys.stderr)

    P6 = 2 ** 6
    P12 = 2 ** 12
    table = [0] * P12
    for s in range(P6):
        if is_valid(0, s):
            for s2 in range(P6):
                if is_valid(1, s) and is_median(0, s, s2):
                    table[s * P6 + s2] = 1

    for y in range(2, 18):
        newtable = [0] * P12
        for s in range(P6):
            if not is_valid(y, s):
                continue
            for past in range(P12):
                if table[past] == 0:
                    continue
                p1, p2 = divmod(past, P6)
                if is_median(p1, p2, s):
                    newtable[p2 * P6 + s] += table[past]
        table = newtable
    return sum(table)
```


