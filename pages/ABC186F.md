---
title: "ABC186F"
---

from [[ABC186]]
ABC186F
- ![image](https://gyazo.com/ecac49bfec2162e0a6e196eff9d3cd89/thumb/1000)
- [F - Rook on Grid](https://atcoder.jp/contests/abc186/tasks/abc186_f)
- かきかけ
- 考えたこと
    - タテヨコでたどり着く方法とヨコタテでたどり着く方法がある
    - 個別に数えて足すと2通りの方法でたどり着けるところがダブルカウントになる
    - ダブルカウントのものの効率良い数え方を考える
    - [[余事象を引く]]方が楽ではないか？
        - つまり「たどり着けないマスを数えて全体から引く
        - ![image](https://gyazo.com/0bfc6272ea8fb38766722b788bda44bb/thumb/1000)
        - この交点が「たどりつけないマス」
    - 各xにおける最小のyを`minY[x]`とする
        - 欲しいのは`minY[x] < y`の範囲にある`minX[y] <= x`の数
    - こういうパターン、見たことがあるぞ…
        - Scrapboxから関連しそうなものを探す
            - [[削除可能集合で不等号条件]]
            - [[ACL1A]]
        - 今回の目的と完全には一致しないが以下の要素は使えそう
            - [[フェニック木]]を使う
            - 値域は0/1で、値の存在不在を表現
    - まとめた [[長方形区間カウント]]
    - 素朴に`minY[x] < y`の範囲にある`minX[y] <= x`の数を数えるコードを書き、同じ結果になるようにフェニック木を使うバージョンを実装
    - 提出→WA
    - 素朴実装とフェニック木実装の食い違いをランダムテストで調べているうちに、素朴実装が間違っていることに気づいた
        - こういうパターン
        - ![image](https://gyazo.com/3fc29bf88b7be3fcc5ccbe6a7b25690e/thumb/1000)
- 公式解説
    - フェニック木を使う方針はOK
    - たどり着けないところを数えるのではなく2通りでたどり着けるところを数えている
    - AC
python

```
def solve(H, W, M, PS):
    minX = [H] * W
    minY = [W] * H
    for x, y in PS:
        minX[y - 1] = min(minX[y - 1], x - 1)
        minY[x - 1] = min(minY[x - 1], y - 1)

    ret = 0
    # horizontal -> vertical
    for x in range(0, minX[0]):
        ret += minY[x]

    # grouping
    from collections import defaultdict
    P2 = defaultdict(list)
    for i in range(M):
        x, y = PS[i]
        P2[y - 1].append(x - 1)

    bit_init(H + 1)
    x0 = minX[0]
    for y in range(0, minY[0]):
        x1 = minX[y]
        if x1 > x0:
            ret += x1 - x0
            x1 = x0
        ret += bit_sum(x1)
        for x in P2[y]:
            bit_set(x, 1)

    return ret
```


