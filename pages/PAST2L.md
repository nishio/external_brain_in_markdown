---
title: "PAST2L"
---

from [[第二回 アルゴリズム実技検定]]
PAST2L

![image](https://gyazo.com/c664b1d0acb09d62cb4f03914e6ca3ca/thumb/1000)
[L - 辞書順最小](https://atcoder.jp/contests/past202004-open/tasks/past202004_l)
- 考えたこと
    - 最初の文字として選ぶことが可能な範囲が一つ定まる
    - 最初の文字はその中の最小のものだ
    - 最小が複数あったら？
        - 最も早いものを選べば良い
        - それ以外を先頭として辞書順最小のがもし存在するなら、先頭を最も早いものに入れ替えても辞書順最小なので。
    - 先頭1文字を決めると、2文字目として選べる範囲が決まる
        - これを繰り返せば良い
- 公式解説
    - 具体的な実装に関して上記だとTLEの可能性がある
- 改めて考えたこと
    - 一旦TLEになってみる
    - それから高速化の方法を考える
    - 範囲に対するargminを効率よく計算できるといい
        - [[Disjoint Sparse Table]]か？
- sample AC
python

```
def solve(N, K, D, AS):
    end = N - D * (K - 1)
    start = 0
    ret = []
    for _i in range(K):
        subseq = AS[start:end]
        if not subseq:
            return [-1]
        v = min(subseq)
        ret.append(v)
        start = AS.index(v, start) + D
        end += D
    return ret
```

    - 8 TLE
- ここから高速化するとなると、やっぱり[[Disjoint Sparse Table]]かなー
- 範囲が後ろにずれていくだけなので[[優先度キュー]]でよい
    - 無効になった値を読み飛ばすスタイル
    - [[スライドRange Argminを優先度キューで]]
- AC
python

```
def solve(N, K, D, AS):
    from heapq import heappush, heappop, heapify
    end = N - D * (K - 1)
    start = 0
    ret = []
    queue = [(AS[i], i) for i in range(start, end)]
    heapify(queue)
    for _i in range(K):
        if start >= end:
            return [-1]
        while True:
            v, i = heappop(queue)
            if start <= i < end:
                break
        ret.append(v)
        start = i + D
        for i in range(end, min(end + D, N)):
            heappush(queue, (AS[i], i))
        end += D
    return ret
```


