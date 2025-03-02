---
title: "DP L"
---

[L - Deque](https://atcoder.jp/contests/dp/tasks/dp_l)
- 対戦ゲームの読み切り問題
- 盤面を定義域とするDP
    - 盤面は範囲で表現できる
- 先手後手を区別する必要はない
    - 先手も後手も「自分の得点-相手の得点」を最大化する
- メモ化してない素朴な再帰
    - サンプルコードは全部成功する
python

```
def solve(N, XS):
    def first(L, R):
        # debug(": L, R", L, R)
        if L == R:
            return XS[L]
        return max(
            XS[L] - first(L + 1, R),
            XS[R] - first(L, R - 1)
        )

    return first(0, N - 1)
```


このままではTLEなのでCythonでコンパイルする
- 「計算が済んでないことを確認するために取りえない値を入れておく」が、正負両方取りうるので計算済みかどうかを持つ配列も作った
    - 十分大きい値にしておく手もあったな
- boolを使うとエラーなのでintにしといた
cython

```
cdef long[3000 * 3000] memo
cdef int[3000 * 3000] done

cdef first(L, R):
    if L == R:
        return XS[L]
    pos = L * N + R
    if done[pos + N]:
        right = memo[pos + N]
    else:
        right = first(L + 1, R)

    if done[pos - 1]:
        left = memo[pos - 1]
    else:
        left = first(L, R - 1)

    ret = XS[L] - right
    x = XS[R] - left
    if x > ret:
        ret = x
    memo[pos] = ret
    done[pos] = True
    return ret


cdef solve():
    for i in range(N * N):
        memo[i] = 0
        done[i] = False

    return first(0, N - 1)


def main():
    global N, XS
    # parse input
    N = int(input())
    XS = list(map(int, input().split()))
    print(solve())
```

[https://atcoder.jp/contests/dp/submissions/15060096](https://atcoder.jp/contests/dp/submissions/15060096)
