
縦横の線分が2000本与えられて10^9くらい広い空間が区切られてる時に、原点から到達可能な範囲の面積を求める[問題](https://atcoder.jp/contests/abc168/tasks/abc168_f)

まとめ
- [[座標圧縮]]してDFSするだけで手元ではAC
- サブミットするとTLE
- maspyさんのコードを参考に事前にグラフを構築したがMLE
- MLEの原因はデンスな行列で表現されてるグラフかと思ったが違った
    - DFSの過程で訪問済み頂点を記録していたsetだった　[[setはメモリ食い]]

-----
コンテスト中にはまったく手付かず。解説を読んでから挑戦

1ピクセルずつ探索すると遅いので意味のある長方形のマス目に刻んで処理する。
- [[座標圧縮]]という言葉で言及されてる。
- 出現する値をsort、uniqueして、それに対して各値をbisectしたら良い。

最初に書いたもの。
- サブミット結果、11/96 TLE [https://atcoder.jp/contests/abc168/submissions/14612194](https://atcoder.jp/contests/abc168/submissions/14612194)
    - これは当然だと思う。座標をリアル座標で持ってて、隣の頂点を探すのに毎回bisectしてるから。
    - 最初にbisectして使うことにしよう
- 後で手元で検証したらAC: 96, max_time: 56.97だった
    - 計算結果は正しかったが、遅すぎた
python

```
N, M = map(int, input().split())
vlines = defaultdict(list)
hlines = defaultdict(list)
vticks = {0}
hticks = {0}

for i in range(N):
    A, B, C = map(int, input().split())
    vlines[C].append((A, B))
    hticks.add(C)
    vticks.update((A, B))

for i in range(M):
    D, E, F = map(int, input().split())
    hlines[D].append((E, F))
    vticks.add(D)
    hticks.update((E, F))

vticks = [-INF] + list(sorted(vticks)) + [INF, INF]
hticks = [-INF] + list(sorted(hticks)) + [INF, INF]


def up(y):
    return vticks[bisect.bisect_left(vticks, y) - 1]


def down(y):
    return vticks[bisect.bisect_left(vticks, y) + 1]


def left(x):
    return hticks[bisect.bisect_left(hticks, x) - 1]


def right(x):
    return hticks[bisect.bisect_left(hticks, x) + 1]


def area(x, y):
    i = bisect.bisect_left(hticks, x)
    width = hticks[i + 1] - hticks[i]
    j = bisect.bisect_left(vticks, y)
    height = vticks[j + 1] - vticks[j]
    return width * height


total_area = 0
visited = set()


def visit(x, y):
    global total_area
    if (x, y) in visited:
        return
    # dp("visited: x,y", x, y)
    a = area(x, y)
    total_area += a
    visited.add((x, y))
    # visit neighbors
    l = left(x)
    if (l, y) not in visited:
        for a, b in vlines[x]:
            if a <= y < b:
                # blocked
                break
        else:
            # can move left
            to_visit.append((l, y))

    u = up(y)
    if (x, u) not in visited:
        for a, b in hlines[y]:
            if a <= x < b:
                # blocked
                break
        else:
            # can move up
            to_visit.append((x, u))

    r = right(x)
    if (r, y) not in visited:
        for a, b in vlines[r]:
            if a <= y < b:
                # blocked
                break
        else:
            # can move left
            to_visit.append((r, y))

    d = down(y)
    if (x, d) not in visited:
        for a, b in hlines[d]:
            if a <= x < b:
                # blocked
                break
        else:
            # can move up
            to_visit.append((x, d)) 

to_visit = [(0, 0)]
while to_visit:
    x, y = to_visit.pop()
    if x == INF or x == -INF or y == INF or y == -INF:
        print("INF")
        break
    visit(x, y)
else:
    print(total_area)
```


事前にbisectする方針(ちゃんと座標圧縮)
- xとyを取り違えて範囲外アクセスでRE
    - 修正したけど同じく11 TLE
    - うーん[[numba]]にするか。

numbaでクロージャに関するエラー
- どういう条件で起こるのかよくわかってない
- visitをなんとなく関数にしてたが、再帰呼び出しするわけでもないのでインライン展開した

`int => [(int, int)]` の形でデータを持ってるのがnumbaワールドに入れにくくて困る
- 自前でnp.arrayに詰め替えた
- 手元では実行できてだいたいACなのだけど一部WAになる
    - 追記: 原因は0を座標に追加し忘れてることで、bisectした時に期待と違うマスに入ってしまうこと
python

```
>>> xs = [-1, 1, 2]
>>> xs[bisect.bisect_left(xs, 0)]
1
```

    - ![image](https://gyazo.com/089dd5c0366f3fd127dcb989cdf2f247/thumb/1000)

    - 最初のコードではちゃんとケアして初期化してるからAC。numbaへの移植過程で壊した。
python

```
 vticks = {0}
 hticks = {0}
```

    - この時点では原因に気付いてなくて、別の渡し方を模索(下記)

[[numbaに複雑な型を渡す]]
- dictやlistも渡せるぞ！
- [[numba bisect]]
    - 標準ライブラリのbisectはそのままでは動かないので mainの中にコピペした
    - この場合は関数内関数なのにちゃんと動くなぁ
- サブミット: all RE
    - atcoderのnumbaは0.48と古いのでtyped.Listが引数を取れないorz
    - こんなことをやるべきではない
        - 「最新版ではできるけど、atcoderのはバージョンが古いから、こう書き換える必要がある」という知識は他に応用が効かない上に、atcoderのバージョンアップとともに陳腐化するタイプの知識、頑張るべきでない
        - 些細なバージョン違いで挙動が変わるようなところは、今後も変わる可能性が高く、陳腐化しやすい知識

他の人の解説やコードを読む
- [https://maspypy.com/atcoder-参加感想-2020-05-18abc-168](https://maspypy.com/atcoder-参加感想-2020-05-18abc-168)
    - [チューニング済みのコード](https://atcoder.jp/contests/abc168/submissions/13389928)
    - [ブログ掲載コード](https://atcoder.jp/contests/abc168/submissions/13359130)
    - [最初のAC](https://atcoder.jp/contests/abc168/submissions/13349468)
- `data = np.int64(read().split())`
    - ああー、なるほど。構造を作ってからそれをどうやって渡そうと考えるからややこしいのであって、読んだままの列として渡すのか…
- [[numpy.unique]]
    - setに似てるがソートされた配列になる
- データ構造
    - 僕の実装は隣接マスへの移動のたびに「その線上にある線分とぶつかるか？」をチェックしてる
        - だから「線上にある線分」を持つ`int => [(int, int)]`があって、それをnumba化するのに苦労してた
    - maspyさんのコードは、長方形に並んだ頂点を持つグラフ構造 #長方形グラフ探索
        - x,yを整数にパックするので`int[:, :]`
            - 頂点あたりの辺の数も4本で固定
            - Q:長方形の端はどうするの？
                - A:端に[[番兵]]を置いてて、到達時点でINFを返して探索終了なので、正しい値が入ってる必要がない
        - 僕はなんとなく「陽にグラフを構築するのは無理」と思い込んでた
        - これくらいの規模(3000 * 3000 * 4)なら問題はないようだ。
        - 工夫すると1000 * 1000 * 4になる
            - [チューニング済みのコード](https://atcoder.jp/contests/abc168/submissions/13389928)では線分の端を刈り込んでいる
            - ![image](https://gyazo.com/7006b27454eb8b4aaa230b1e3c7e1fa8/thumb/1000)

次にやること
- 複雑な型をnumbaに渡すのはやめる
- 今と同じ複雑な型をnumba世界で構築できるか試す

`vlines[C] = []`
python

```
There are 10 candidate implementations:
   - Of which 8 did not match due to:
   Overload in function 'setitem': File: <built-in>: Line <N/A>.
     With argument(s): '(DictType[undefined,undefined], int64, list(undefined))':
    No match.
   - Of which 2 did not match due to:
   Overload in function 'impl_setitem': File: numba/typed/dictobject.py: Line 669.
     With argument(s): '(DictType[undefined,undefined], int64, list(undefined))':
    Rejected as the implementation raised a specific error:
      TypingError: list(undefined) as value is forbidden
```

`vlines[C] = [(0, 0)]`
`TypingError: list(UniTuple(int64 x 2)) as value is forbidden`

ダメだ、numbaで複雑な型を使うのは諦めよう。

numbaの細かい話
python

```
# OK 
xticks = np.unique(np.concatenate((A, B, D, np.array([-INF, 0, INF]))))
# NG
yticks = np.unique(np.concatenate((E, F, C, [-INF, 0, INF])))
```

- 下のコードはnp.concatenateの引数のタプルに型が混在しているためエラーになる see [[numba np.concatenate]]

`AC: 25, WA: 65, RE: 6, max_time: 0.53`
- 横線の書き方を勘違いしてた
- REはSegmentation fault

`AC: 96, max_time: 2.91`
- submit
    - sub1_93.txt	MLE
    - メモリ制限にぶつかるの初めての経験だ
    - 初めてなので対処法もよく分からないが、グラフを作り終わったらA〜Fは必要ないから捨ててみるかな？
    - ダメです
    - グラフのエッジをintではなくboolにしてみる
    - これでもダメか！
    - scipy.sparse.[[csr_matrix]]を使ってみたがnumbaがサポートしてない

改めてmaspyさんのコードを読み直してみると
- [チューニング済みのコード](https://atcoder.jp/contests/abc168/submissions/13389928)は素直に4*Nの行列で待っているが
- [最初のAC](https://atcoder.jp/contests/abc168/submissions/13349468)では頂点ペアの2*|E|で持ってる？
python

```
def add(v, w):
    nonlocal p
    nxt[p] = head[v]
    head[v] = p
    ng[p] = w
    p += 1
```

    - あー、なるほど、これ[[リンクトリスト]]か！
        - pが空き位置
        - vについて前に書き込んだところが`head[p]`に入っているのでそれを`next[p]`に転記することでリンクをつなげる
        - headは-1で初期化されているので-1が末端
        - ![image](https://gyazo.com/cd9568515772bf6b0b7aeb340b69bc4d/thumb/1000)

- [最初のAC](https://atcoder.jp/contests/abc168/submissions/13349468)はこの工夫をして227MB
- [ブログ掲載コード](https://atcoder.jp/contests/abc168/submissions/13359130)は素直なboolの行列で86MB
- 一方僕は1532MB…

わからぬ…
- 最初のコードはリンクトリストにしてるから省メモリ
- チューニング済みコードは線分の端を落としてるから超点数が1/9に減って省メモリ
- しかしブログのコードは普通に9_000_000 * 4のデンスなnp.array。
    - 僕のコードと同じ
    - 多少の差ならまだしも、20倍も差があるのはなぜ？？

- `solve(*precompute(N, M, data))`って二段構えになっていること
    - 関係ない
- 整数を64ビットではなく32ビットで持つ
    - `10 ** 9 < 2 ** 31`
    - 解決しない
- 座標圧縮済みの値を16ビットで持つ
    - `3000 < 2 ** 15`
    - 解決しない
- グラフをN * 4で持つ代わりに4つの値を整数にパックしてuint8で持つ
    - 解決しない
- `INF = 10 ** 9 + 1`
    - 僕は`INF = 10 ** 10`にしてたがこれは実はInt32.MaxValueを超えてる
    - `10 ** 10 > 2 ** 31`
    - 変えてみたけど影響なし

全然解決しないので手元で[[mprof]]してみる
- 自分のコード
    - ![image](https://gyazo.com/b7f0e30e84651d516ec7d6e0e824edfc/thumb/1000)
- maspyさんのコード
    - ![image](https://gyazo.com/2be679307b2e46e272231527258c0d8d/thumb/1000)
- うーむ、確かにメモリを食っている


頂点数を調べたらどちらも(9018009, 4)だったので、バグによって頂点数が爆増しているわけではない

あっ、わかった
- 原因はグラフの構築ではない
- DFSの過程で訪問済み頂点を記録していたsetだ
python

```
x = set()
for i in range(9_000_000):
    x.add(i)
```

- ![image](https://gyazo.com/afd0afef705664b82f9b3628c428add9/thumb/1000)
- [[setはメモリ食い]]
    - 1エントリーあたり90バイトも食っている
    - サイズ4Nのグラフのことばかり気にしていたけど、サイズNのsetが数十倍の係数で乗っかってたのか
    - np.zerosに置き換えてAC [https://atcoder.jp/contests/abc168/submissions/14647413](https://atcoder.jp/contests/abc168/submissions/14647413)
        - ![image](https://gyazo.com/45ec66aaf39e1d10441d5ff68e6fae69/thumb/1000)

敗因考察
- 事前にグラフを構築する実装に変えてMLEになったのでグラフが悪いと思い込んだ
    - 直近で変えたところに問題があるという思い込み
    - 実際は前の実装はTLEだったので、MLEになる前に時間が尽きてただけである
- mprofには行ごとにメモリ消費量を出す機能がある。これを早い段階で使っていれば問題がグラフ構築にないことに気づけたはず。
    - numbaでコンパイルしてるから〜と思って試してなかった
- 試行錯誤の過程
    - ![image](https://gyazo.com/0caddaabf0befdb5c74626f7f6dae131/thumb/1000)
    - MLEだけに注目して「全然解決しない！」と思っていたが、消費メモリはちゃんと減っていた
    - 「修正によってメモリ消費が減ったが、全体の中の割合としては大したことがない」ってのは「いま注目してるところ以外にメモリを食う原因がある」ということに他ならない
    - このタイミングで気付いて、何がメモリを食っているのか[[mprof]]で調査するべきだった

大きいデータだと時間がかかりすぎ、小さいデータだとメモリ消費が小さすぎてよくわからない
程よいのを見つけた(下記)
コンテスト中に見つけるのは難しそうなので、MLEになりそうなコードをそもそも書かないことが大事そう
:

```
2510957991
Filename: f_mle.py

Line #    Mem usage    Increment   Line Contents
================================================
    24   79.117 MiB   79.117 MiB   @profile
    25                             def main(N, M, data):
...
    40   79.223 MiB    0.105 MiB       xticks = np.unique(np.concatenate((E, F, C, np.array([-INF, 0, INF]))))
    41   79.223 MiB    0.000 MiB       yticks = np.unique(np.concatenate((A, B, D, np.array([-INF, 0, INF]))))
    42   79.230 MiB    0.008 MiB       width = xticks[1:] - xticks[:-1]
    43   79.230 MiB    0.000 MiB       height = yticks[1:] - yticks[:-1]
    44                             
    45                                 # compress
    46   79.238 MiB    0.008 MiB       A = np.searchsorted(yticks, A)
...
    56                             
    57   79.266 MiB    0.027 MiB       ng_egdes = np.zeros((NUM_VERTEXES, 4), dtype=np.bool_)
    87   79.484 MiB    0.000 MiB       while to_visit:
...
    88   79.484 MiB    0.000 MiB           pos = to_visit.pop()
    89   79.484 MiB    0.004 MiB           y, x = divmod(pos, GRAPH_WIDTH)
    90   79.484 MiB    0.012 MiB           if pos in visited:
...
    96   79.484 MiB    0.000 MiB           total_area += width[x] * height[y]
    97   79.484 MiB    0.125 MiB           visited.add(pos)
    98                                     # plan to visit neighbors
    99   79.484 MiB    0.000 MiB           for i in range(4):
   100   79.484 MiB    0.012 MiB               if not ng_egdes[pos, i]:
   101   79.484 MiB    0.008 MiB                   to_visit.append(pos + direction[i])
   102                                 else:
   103   79.484 MiB    0.000 MiB           print(total_area)
```


[[atcoder]]
