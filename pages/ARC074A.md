
[C - Chocolate Bar](https://atcoder.jp/contests/arc074/tasks/arc074_a)
- ![image](https://gyazo.com/e5a08f96669cd40e7509f03bf2e5fd9d/thumb/1000)
- 考えたこと
    - 縦横どちらかが3の倍数なら三等分すれば良い
    - 1と2に分けてから2の方を分割する時、可能なら二等分が最適
        - それ以外では遠い方がより遠ざかるから
    - 1/3のfloorかceilであると言えるか？
        - 二等分ができるなら言えるけど…
        - floorかceilのどちらかでは二等分ができる
            - それじゃ堂々巡りか
        - 二等分できなくても成り立ちそう
            - ある分割と1/3の間に別の分割yがある時、常にyの方が優れている
            - …うーん、場合わけがいっぱいあって面倒だな
- AC
python

```
def solve(H, W):
    if W % 3 == 0:
        return 0

    def f(x):
        ret = []
        a1 = H * x
        if H % 2 == 0:
            a2 = (H // 2) * (W - x)
            ret.append(abs(a2 - a1))
        elif (W - x) % 2 == 0:
            a2 = H * ((W - x) // 2)
            ret.append(abs(a2 - a1))
        else:
            ar = H * (W - x)
            a2 = H // 2 * (W - x)
            a3 = ar - a2
            ret.append(max(a1, a2, a3) - min(a1, a2, a3))
            a2 = H * ((W - x) // 2)
            a3 = ar - a2
            ret.append(max(a1, a2, a3) - min(a1, a2, a3))
        return min(ret)

    return min(f(W // 3), f(W // 3 + 1))


def main():
    H, W = map(int, input().split())
    print(min(solve(H, W), solve(W, H)))
```

- 公式解説
    - 片方を全探索して、もう片方は縦分割と横分割のそれぞれについてfloorで決めてる

python

```
def solve(H, W):
    if W % 3 == 0:
        return 0

    def f(x):
        ret = []
        a1 = H * x
        ar = H * (W - x)
        a2 = H // 2 * (W - x)
        a3 = ar - a2
        ret.append(max(a1, a2, a3) - min(a1, a2, a3))
        a2 = H * ((W - x) // 2)
        a3 = ar - a2
        ret.append(max(a1, a2, a3) - min(a1, a2, a3))
        return min(ret)

    return min(f(W // 3), f(W // 3 + 1))


def main():
    H, W = map(int, input().split())
    print(min(solve(H, W), solve(W, H)))
```

