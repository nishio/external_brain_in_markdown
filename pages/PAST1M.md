
[M - おまかせ](https://atcoder.jp/contests/past201912-open/tasks/past201912_m)
![image](https://gyazo.com/6e7b0970c5ef90359fec6baba959c845/thumb/1000)

- 考えたこと
    - 比率を最大化する選び方を探す問題
    - 比率の大小関係に関して何かあるかな
    - 3/1と200/100では前者が大きいが、0/100を足すと後者の方が大きい
    - [http://www.asahi-net.or.jp/~vd7t-ktgw/other_favorites/programmingcontest/ProgrammingContest.html](http://www.asahi-net.or.jp/~vd7t-ktgw/other_favorites/programmingcontest/ProgrammingContest.html)
        - 比率に関するDP問題
            - [https://atcoder.jp/contests/abc054/tasks/abc054_d](https://atcoder.jp/contests/abc054/tasks/abc054_d)
        - 今回は値の範囲が10^5だから無理だな
- 公式解説
    - 比率を直接最大化するのではなく、比率がXを超えるかの判定問題にする
    - これはO(NlogN)で判定できる
    - 比率の取りうる範囲について二分探索すればよい
    - [[和の比率の最大化]]
- 時間をおいて考えたこと
    - Nが1000なので2^Nの全探索は無理
    - 貪欲に「大きくなるものを足していく」ではダメか？
        - 「X1 < X1 + X2 なら X1 + X3 < X1 + X2 + X3」ならOK
python

```
from random import randint
for i in range(1000):
    a, b, c, d, e, f = [randint(1, 10) for i in range(6)]
    if a / b < (a + c) / (b + d) and (a + e) / (b + f) > (a + c + e) / (b + d + f):
        print(a, b, c, d, e, f)
        break
```

        - 反例あっさり見つかった: 5 8 5 7 8 7
    - [[和の比率の最大化]]をベースに考える
    - Xを超えるかどうかの判定問題にする
        - $B_i - X A_i$の符号判定問題
        - Mから最大のものを1つ選ぶ
            - すべて負なら「選ばない」の0が最大
        - ソートして最も大きいものが正ならOK
        - [[二分探索]]
- 3WA
python

```
def solve(N, M, AS, BS, CS, DS):
    left = 0.0
    right = 1000000.0
    while left < right - 10 ** -7:
        x = (left + right) / 2
        y = max(DS[i] - x * CS[i] for i in range(M))
        zs = list(sorted([BS[i] - x * AS[i] for i in range(N)], reverse=True))
        if y > 0:
            y = y + sum(zs[:4])
        else:
            y = sum(zs[:5])

        if y >= 0:
            left = x
        else:
            right = x
    return left
```

    - rightは10001で良いはず、多めに1000000にしたが変化なし
    - left < right - 10 ** -7は要求されてる10 ** -6より小さくしてある
    - あ、わかった `if y > 0:`→ `if y > zs[4]:`か
        - →AC
        - 最良のお助けが負のスコアの時「得しないから使わなくて良い」と判断したが「5匹選ばなければならない」という制約によりお助けを選ばない場合にはzs4が選ばれることになるので、こちらがもっと大きなマイナスである可能性がある



[[誤差を認める問題→二分探索]]
[[第一回 アルゴリズム実技検定]]
