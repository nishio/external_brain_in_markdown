
from [[第三回 アルゴリズム実技検定]]
PAST3I
- 正方行列に対して、転置、行交換、列交換、特定の升目の値を表示、などのコマンドを繰り返し実行する問題。
- 問題条件で、行列の大きさが最大で10万になるので、素朴に行列を持つのは選択肢として有り得ないのがわかる。
- 最初に考えたアルゴリズムは「表示命令から時間軸逆順にたどれば、ひとつのマスのことだけ考えれば良いから楽」
    - しかしタイムリミット超過して、これではダメだと気づく。
    - 十分にシンプルなプログラムだったので、そのアルゴリズムのまま高速化することでは解決できないと気づけた。
- おそらく「コマンド列が最長の10万で、半分くらい表示命令だった時に12億回程度のステップが必要」ってことだろう。
    - そう考えてそれをテストケースに追加。
- 行列を「今の行、列が、元々はどの行、列か」と言う情報に分解して持つことにする。
    - [[転置は1ビットのフラグ]]があれば良い。
python

```
if 1:
    N = int(input())
    Q = int(input())
    queries = []
    for i in range(Q):
        queries.append([int(x) for x in input().split()])
else:
    N = 100000
    queries = [
        [2, 1, 2],
        [4, 1, 2]
    ] * 10000
    queries.append([4, 1, 2])
    Q = len(queries)


isTransposed = False
xs = list(range(N + 1))
ys = list(range(N + 1))

for q in queries:
    f = q[0]
    if f == 4:
        i, j = q[1:]
        if isTransposed:
            i, j = j, i
        print(N * (xs[i] - 1) + ys[j] - 1)
    elif f == 3:
        isTransposed = not isTransposed
    else:
        i, j = q[1:]
        if (f == 1) ^ isTransposed:
            xs[i], xs[j] = xs[j], xs[i]
        else:
            ys[i], ys[j] = ys[j], ys[i]
```

