---
title: "メモ化再帰DPでTLEを避けるには"
---

- 再帰呼び出しで実装するのが自然な問題がある
    - 例えば、たどる順序が自明でない動的計画法を[[メモ化再帰]]呼び出しで実装するシチュエーション
- Pythonは数値演算が重いので演算の多い動的計画法はTLEしやすい
- PyPyだと関数呼び出しが遅いので再帰呼び出しを酷使するとTLEしやすい
    - [[PyPyの関数呼び出しは遅い]]
- 普段はNumbaでAOTコンパイルして高速化してるのだけど…
    - Numbaは関数内関数の再帰呼び出しをサポートしてない
    - 関数外に置いてもAOTではできない
    - JITならできるが実行フェーズにコンパイルするので速度上不利
- Cythonだと関数を「Cからしか呼ばれない」と明示してコンパイルできるので有効打になり得る？
    - →現時点で最速

ターゲット問題としてグラフの最長パスを見つける[G - Longest Path](https://atcoder.jp/contests/dp/tasks/dp_g)を使う
- 速度の比較にはAtCoderのサーバ上でのテストケース1_17, 1_01の実行速度を使う
    - 1_01が一番大きいが、タイムアウトすると時間が分からないので一回り小さい1_17も併用した

実行時間まとめ
| 1_17 | 1_01 |
| -- | -- | -- | -- |
| 653 ms | TLE | Code1 Python | 素朴なメモ化再帰 |
| 422 ms | TLE | Code1 PyPy |
| 735 ms | TLE | Code2 Python | メモ化 dict→list |
| 378 ms | 485 ms | Code2 PyPy |
| 434 ms | 565 ms | Code3 Python | 関数呼び出し前に計算済みかをチェック |
| 498 ms | 352 ms | Code3 PyPy |
| 169 ms | 223 ms | Code4 Cython |
| 142 ms | 177 ms | Code5 Cython | メモ化 array→Cの配列 |
| 148 ms | 164 ms (best) | Code6 Cython | 探索終了条件分岐を再帰の外で先に済ませる |
| 1209 ms | 1225 ms | Code7 Numba | JIT |
| 295 ms | 368 ms | Code8 Python | 深さ優先探索の帰りがけ順で処理 |
| 253 ms | 256 ms | Code8 PyPy |


Code1: 素朴なメモ化再帰
- Python 653 ms TLE [https://atcoder.jp/contests/dp/submissions/14906600](https://atcoder.jp/contests/dp/submissions/14906600)
- PyPy 422 ms TLE [https://atcoder.jp/contests/dp/submissions/14906630](https://atcoder.jp/contests/dp/submissions/14906630)
python

```
from collections import defaultdict
import sys

sys.setrecursionlimit(10**6)


def solve(N, M, edges):
    longest = {}

    def get_longest(start):
        if start in longest:
            return longest[start]

        next_edges = edges.get(start)
        if not next_edges:
            ret = 0
        else:
            ret = max(get_longest(v) for v in edges[start]) + 1
        longest[start] = ret
        return ret

    return max(get_longest(v) for v in edges)


def main():
    N, M = map(int, input().split())
    edges = defaultdict(set)
    for i in range(M):
        v1, v2 = map(int, input().split())
        edges[v1].add(v2)

    print(solve(N, M, edges))


main()
```


Code2: メモ化にdictを使ってることを疑問に思う人がいるかもしれないのでlistに変えたバージョン
- Python  735 ms TLE  [https://atcoder.jp/contests/dp/submissions/14907532](https://atcoder.jp/contests/dp/submissions/14907532)
- PyPy 378 ms AC 1_01: 485 ms [https://atcoder.jp/contests/dp/submissions/14907612](https://atcoder.jp/contests/dp/submissions/14907612)
- この感じだとPyPyがdictへのアクセスが苦手な可能性があるな(要検証)
python

```
def solve(N, M, edges):
    longest = [-1] * (N + 1)
    for i in range(N + 1):
        if not edges[i]:
            longest[i] = 0

    def get_longest(start):
        ret = longest[start]
        if ret != -1:
            return ret

        next_edges = edges.get(start)
        if not next_edges:
            ret = 0
        else:
            ret = max(get_longest(v) for v in edges[start]) + 1
        longest[start] = ret
        return ret

    return max(get_longest(v) for v in edges)
```


Code3 関数呼び出し前に計算済みかどうかをチェックするバージョン
- Python 434 ms / 565 ms [https://atcoder.jp/contests/dp/submissions/14916958](https://atcoder.jp/contests/dp/submissions/14916958)
- PyPy 498 ms / 352 ms [https://atcoder.jp/contests/dp/submissions/14907832](https://atcoder.jp/contests/dp/submissions/14907832)
- 関数呼び出しの回数をラスト1回分減らす

Code4 Cython
cython

```
cdef get_longest(long start, dict edges, long[:] longest):
    if longest[start] != -1:
        return longest[start]

    cdef list next_edges
    next_edges = edges.get(start)
    if not next_edges:
        ret = 0
    else:
        #ret = max(get_longest(v, edges, longest) for v in edges[start]) + 1
        ret = 0
        for v in edges[start]:
            x = get_longest(v, edges, longest) + 1
            if x > ret:
                ret = x

    longest[start] = ret
    return ret


def solve(N, M, edges):
    cdef array.array longest = pyarray.array('l', [-1] * (N + 1))
    return max(get_longest(v, edges, longest) for v in edges)	 
```

- AC 169 ms / 223 ms [https://atcoder.jp/contests/dp/submissions/14906046](https://atcoder.jp/contests/dp/submissions/14906046)
- 関数内関数のままではcdefに出来なかったので外に出した
    - [[Cythonでは関数内で関数定義ができない]]
- リストのアクセスが遅そうだったのでarrayに変えた
    - これは関係なさそう see [[Cythonで添え字を型宣言しても速くない]]
- ジェネレータ内包が問題を起こしてたのでforループに書き換えた
    - [[Cythonとジェネレータ内包]]

Code5 longestをCの配列としてグローバルに置く
- 142 ms / 177 ms
- リストでもarrayでもなくC配列が良かったので。関連: [[Cythonで添え字を型宣言しても速くない]]
- [https://atcoder.jp/contests/dp/submissions/14913275](https://atcoder.jp/contests/dp/submissions/14913275)

Code6 出て行く辺があるかどうかの条件分岐を再帰の外で先に済ませる
- 148 ms / 164 ms
- [https://atcoder.jp/contests/dp/submissions/14913765](https://atcoder.jp/contests/dp/submissions/14913765)

Numba
- 速度はさておき何もしなくてもそのまま動くCythonと比べると、Numbaは動くようにするまでが大変
    - `ret = max(get_longest(v) for v in edges[start]) + 1`
        - `The use of yield in a closure is unsupported.`
    - [https://gist.github.com/nishio/dd3013df3e88ef1afb0d41d5980a3882](https://gist.github.com/nishio/dd3013df3e88ef1afb0d41d5980a3882)
        - `Compilation is falling back to object mode WITH looplifting enabled because Function "get_longest" failed type inference due to: non-precise type pyobject`
        - 単純にnumba.jitをつけるアプローチではうまくいかない、型推論ができるオブジェクトを引数にする必要がある
- 隣接リスト形式のグラフの扱いが難関
    - Pythonで気楽に作るとdafaultdict(list)だが、dictもlistも適切でない
    - 可変長なので雑にnp.arrayにすると空間がN * M
    - 整数列として渡してNumba世界で連結リストにするのが一番マシかなと思う
        - 今回の問題ではグラフの辺の最大数が決まってるのでそのサイズのnp.array を確保する

Code7: Numba JIT
- 1209 ms / 1225 ms [https://atcoder.jp/contests/dp/submissions/14915733](https://atcoder.jp/contests/dp/submissions/14915733)
- 今までの中で格段に遅い、よく通ったもんだ
    - しかし二つの問題にかかった時間の差は16msecで、一番速いCython実装と同じぐらい
    - つまりJITであるせいで実行フェーズでコンパイルしてしまい時間を食っているが、コンパイル済みのものは高速ということ
    - 僕が普段NumbaをAOTで使うのもこれが理由。コンパイルフェーズでAOTコンパイルできるなら実行フェーズでJITコンパイルする必要は皆無
- Numba AOTはコンパイル時にエラーになる
    - `Untyped global name 'get_longest': cannot determine Numba type of <class 'function'>`
        - これは再帰呼び出しだと人間が認識しているものが、Pythonにとっては「グローバル変数を取得してそれを呼ぶ」だから。
            - 関数定義の後に同じ名前で別のものに名前が再束縛されるかもしれないので、取得したグローバル変数の型が不明なのである。
            - とはいえこれは不便なので、例えばコンパイル時に「この関数内での同名変数のコールはこの関数自体のコールである」と人間が宣言することで再帰呼び出しを可能にするとかが、将来のNumbaには入るかもしれない、入るといいなぁ
            - JITではできてるんだからAOTできてもいいじゃんー
    - というわけで今のところ末尾再帰でない再帰関数をNumbaでAOTする方法は見つけられていない

Code8: 深さ優先探索の帰りがけ順で処理をする案
- そもそも再帰呼び出しを使わなくてもコールツリーを深さ優先で探索して帰りに処理をすれば良い、という発想
python

```
def solve(N, M, edges):
    longest = {}

    stack = [v for v in edges]

    while stack:
        v = stack.pop()
        if v > 0:
            if v in longest:
                continue
            next_edges = edges.get(v)
            stack.append(-v)
            if next_edges:
                stack.extend(next_edges)
        else:
            next_edges = edges.get(-v)
            if not next_edges:
                ret = 0
            else:
                ret = max(longest[x] for x in next_edges) + 1
            longest[-v] = ret

    return max(longest[v] for v in edges)
```

Python 295 ms / 368 ms [https://atcoder.jp/contests/dp/submissions/14916269](https://atcoder.jp/contests/dp/submissions/14916269)
PyPy 253 ms / 256 ms [https://atcoder.jp/contests/dp/submissions/14916290](https://atcoder.jp/contests/dp/submissions/14916290)
