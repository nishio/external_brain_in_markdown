
from [[第四回 アルゴリズム実技検定]]
PAST4L
[L - マンションの改築](https://atcoder.jp/contests/past202010-open/tasks/past202010_l)
- 考えたこと
    - 奇数、偶数、1点、のいずれかに加算をして、隣接する値の一致するものの数を毎回答える
    - クエリが10^5なので、クエリあたりは定数かlog
    - 1点変更はまあいいとして奇数が問題
        - 偶数番ひく奇数番の差分で持っておけば単なるRange Add
        - Range Addして全体のなかから0のものの個数を探す？？
        - Range Addしないで-xのものを探せばいい
            - 頻度表を配列で持てるなら定数オーダー
            - 10^9なので無理
            - ハッシュでいける？
        - 点更新の時どうする？
            - 逆算する
    - AC
python

```
def main():
    N, Q = map(int, input().split())
    HS = list(map(int, input().split()))
    from collections import defaultdict
    freq = defaultdict(int)
    for i in range(N - 1):
        d = HS[i] - HS[i + 1]  # odd - even
        if i & 1:
            d = -d
        freq[d] += 1

    odd_height = 0
    for _q in range(Q):
        q = list(map(int, input().split()))
        if q[0] == 1:
            odd_height += q[1]
            print(freq[-odd_height])
        elif q[0] == 2:
            odd_height -= q[1]
            print(freq[-odd_height])
        else:
            i = q[1] - 1
            add = q[2]
            if i > 0:
                d = HS[i] - HS[i - 1]
                if i & 1:
                    d = -d
                freq[d] -= 1
            if i < N - 1:
                d = HS[i] - HS[i + 1]
                if i & 1:
                    d = -d
                freq[d] -= 1

            HS[i] += add
            if i > 0:
                d = HS[i] - HS[i - 1]
                if i & 1:
                    d = -d
                freq[d] += 1
            if i < N - 1:
                d = HS[i] - HS[i + 1]
                if i & 1:
                    d = -d
                freq[d] += 1
            print(freq[-odd_height])
```


[[PAST1H]]と似てる
