
[C - 列](https://atcoder.jp/contests/abc032/tasks/abc032_c)
- ![image](https://gyazo.com/47719be25ce60aaeff7678ae9cd28aae/thumb/1000)
- 考えたこと
    - [[しゃくとり法]]？
    - 範囲を伸ばすと積は単調非減少
        - なので、始点を固定して探索したとき、一旦条件を満たさなくなったらそれより長い条件を満たすものはないことがわかる
        - しゃくとり法とは違うか、条件を満たさない時に始点を+1するのは同じだが、今回は「計算結果が最大」ではなく「長さが最大」を要求されてるので範囲を縮める必要はない
            - [[条件を満たす最長の列]]
python

```
if f(start, start + length + 1) <= K:
	length += 1
else:
	start += 1
```

    - これを列の最後に到達するまで回せば良い
    - lengthが長い時に長さの線形オーダーの時間がかかると10^10オーダーになって間に合わないので定数オーダーにする必要がある
        - 累積積の前処理をしてもいいけど、1つ掛けて1つ割れば、あっ気づいた
    - 数列の要素は1以上だと思い込んでだけど、0以上だ
        - つまり0が出現する時、列全体を覆うのが正解
        - 0が出現しない時は、割り算ができるので定数オーダーで範囲の積がけいさんできる
- 公式解説
    - 0を含む場合を除外するのは同じ
    - 2以上の場合長さは対数オーダー
        - 1が続くと困るので圧縮しようって言ってる
        - これでO(N log K)
    - 別解でしゃくとり法を解説してる
- 実装
    - 実装してみたら「縮めないで進む」はちょっと面倒だった
python

```
def solve(N, K, S):
    if 0 in S:
        return N

    start = 0
    result = 0
    end = 1
    prod = S[start]
    while end < N:
        if prod <= K:
            result += 1
            prod = prod * S[end]
            end += 1
        else:
            prod = prod * S[end] // S[start]
            start += 1
            end += 1
    if prod <= K:
        result += 1

    return result
```

- しゃくとり法だと長さが縮むからmaxを取る必要があるね、めんどくささはそれほど変わらなかった
    - こちらにだけK==0のチェックがあるのは、しゃくとり法では縮めたら条件が充足される想定だけど、空の列でも1なのでK==0の時には充足されないから
python

```
def solve(N, K, S):
    if 0 in S:
        return N
    if K == 0:
        return 0

    start = 0
    result = 0
    end = 1
    prod = S[start]
    while end < N:
        if prod <= K:
            result = max(result, end - start)
            prod = prod * S[end]
            end += 1
        else:
            prod = prod // S[start]
            start += 1
    if prod <= K:
        result = max(result, end - start)

    return result
```


