
[F - Contrast](https://atcoder.jp/contests/abc178/tasks/abc178_f)
![image](https://gyazo.com/2f42a5744a2fdfabc0c5a486a12710fd/thumb/1000)

from [[ABC178]]
ABC178F
- リアルタイム
    - 最も余ってる数から使っていけばいいだろ、と実装
        - 24 WA
    - 方針がダメだったのか後で確認
- 公式解説
    - 範囲が重ならないようにずらすことで解が得られる
- 時を置いて考えたこと
    - [[一つ構築せよ問題]]
    - たくさんある解の中から構築しやすいものを見つけることが必要
    - [[貪欲法の証明パターン]]
        - 「解があるならこの形の解がある」
    - まず一番出現回数が多い数に注目する
        - ![image](https://gyazo.com/5e927d1680578778fb5d07f47a5bc7a3/thumb/1000)
        - A: 出現回数CがNを超えてたら明らかに不可能
        - B: ちょうどNの時、重ならないように入れるしかない
            - この時、残りのマスの並びはどうであっても関係ない
        - C: それ以外の場合、N-Cマスを被らないように並べれば良い
            - N個出現する数がない限り配置できる
                - 「出現頻度最大の数を選ぶ」の条件から、そのようなものはないことがわかる
- 実装
    - 20分で実装、25分で手元バグ修正、提出して20WA
        - うーん、どういうパターンを見落としてるのだろう？
        - →for文なのにポインタをインクリメントした時にcontinue
    - ランダムテストでおかしな出力を見つけ、修正して53分で提出、6WA
        - [[ジャッジ結果から情報を得る]]
python

```
assert Counter(BS) == Counter(ret)
return ret
```

        - 6WA
python

```
assert all(AS[i] != ret[i] for i in range(N))
```

        - む？6WA??
python

```
assert len(ret) == N
```

        - むむ？これも6WA？
        - あ、そうか、
python

```
assert 1 == 2
print("No")
```

        - 16RE
        - つまり本当はNoを返すべきでないのに返してるケースがある
python

```
if b_count[b] == 0:
    assert 1 == 2
    return
```

        - 6RE
        - つまりこれが間違い
- →AC
python

```
def solve(N, AS, BS):
    from collections import Counter
    a_count = Counter(AS)
    b_count = Counter(BS)

    max_occur = 0
    when_max = None
    for i in range(N + 10):
        t = a_count[i] + b_count[i]
        if t > N:
            return
        if t > max_occur:
            max_occur = t
            when_max = i

    ret = []
    del a_count[when_max]
    del b_count[when_max]
    a_keys = list(a_count.keys())
    b_keys = list(b_count.keys())
    a_pointer = 0
    b_pointer = 0
    a_len = len(a_keys)
    b_len = len(b_keys)
    for _i in range(N - max_occur):
        a = a_keys[a_pointer]
        if a == when_max:
            a_pointer = (a_pointer + 1) % a_len
            a = a_keys[a_pointer]
        c = a_count[a]
        if c == 0:
            del a_count[a]
            a_pointer = (a_pointer + 1) % a_len
            a = a_keys[a_pointer]

        b = b_keys[b_pointer]
        while a == b or b == when_max or b_count[b] == 0:
            b_pointer = (b_pointer + 1) % b_len
            b = b_keys[b_pointer]

        ret.append((a, b))
        a_count[a] -= 1
        b_count[b] -= 1

    for b in b_count:
        for _i in range(b_count[b]):
            ret.append((when_max, b))
    for a in a_count:
        for _i in range(a_count[a]):
            ret.append((a, when_max))

    ret.sort()
    ret = [b for a, b in ret]
    return ret
```


