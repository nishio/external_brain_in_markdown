
AC

0からスタートして、2倍、3倍、5倍、プラスマイナス1、のいずれかの操作を繰り返してNにする。4種類の操作それぞれにコストが定められており、最小コストを求める[問題](https://atcoder.jp/contests/agc044/tasks/agc044_a)。

問題文の通り0からNを目指すのではなく、Nから0を目指すことにして、選択肢を「2の倍数まで移動して2で割る」「3について同様」「5について同様」「0まで移動する」の4つにすることで「やたらたくさん+1をやって時間を食い潰す」という罠を回避する。[[時間軸反転]]

Nからスタートして「最も大きい未探索の数(頂点)」に上記の4通りの操作をしていく。なぜなら全ての操作は数を減少させるので、最大の数は他にその数に至る選択肢がなく「暫定最小スコア」が真に最小スコアだと確定してるから。

各頂点ごとの「暫定最小スコア」はPythonのdictに入れた。定義域が10^18あるので配列にはしたくないよね。

普段なんとなくINF=10**10とかやって「これで十分だろ」と思ってるのだけど、この問題Nが最大10^18、各コストが最大10^9なのであっさり超えてしまう。微妙にWAする。いくらが理論上の最大値なのか考えてないけど、十分大きな数にしておく。

ピュアPythonでAC
python

```
INF = 10 ** 27 + 1
def solve(N, A, B, C, D):
    to_visit = [-N]
    cost = {N: 0}

    def put(n, c):
        cost[n] = min(cost.get(n, INF), c)
        heappush(to_visit, -n)

    visited = N + 1
    while to_visit:
        n = -heappop(to_visit)
        if n == visited:
            continue

        visited = n
        c = cost[n]
        put(0, c + n * D)

        if n % 2 == 0:
            put(n // 2, c + A)
        else:
            put((n+1) // 2, c + A + D)
            put((n-1) // 2, c + A + D)

        if n % 3 == 0:
            put(n // 3, c + B)
        elif n % 3 == 1:
            put((n-1) // 3, c + B + D)
            put((n+2) // 3, c + B + D * 2)
        else:
            put((n+1) // 3, c + B + D)
            put((n-2) // 3, c + B + D * 2)

        if n % 5 == 0:
            put(n // 5, c + C)
        elif n % 5 == 1:
            put((n-1) // 5, c + C + D)
            put((n+4) // 5, c + C + D * 4)
        elif n % 5 == 2:
            put((n-2) // 5, c + C + D * 2)
            put((n+3) // 5, c + C + D * 3)
        elif n % 5 == 3:
            put((n+2) // 5, c + C + D * 2)
            put((n-3) // 5, c + C + D * 3)
        elif n % 5 == 4:
            put((n+1) // 5, c + C + D)
            put((n-4) // 5, c + C + D * 4)

    return cost[0]
```

[https://atcoder.jp/contests/agc044/submissions/14679372](https://atcoder.jp/contests/agc044/submissions/14679372)


[[桁DP]]
[[AGC044]] [[atcoder]]
