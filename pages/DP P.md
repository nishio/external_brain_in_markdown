
[P - Independent Set](https://atcoder.jp/contests/dp/tasks/dp_p)
- 与えられた木を白黒で塗り分ける、黒い頂点は隣接してはいけない、何通りあるか数え上げよ、という問題
- 直線的な依存関係の時に「端から順に」「直前だけ見て」DPができたのと同様に、木構造の依存関係の時には「葉から順に」「木の根だけ見て」DPができる　[[木DP]]
- ![image](https://gyazo.com/10a0e781f27b7b7fc988257afad814b8/thumb/1000)
- 木をたどるところで再帰を使っているが、対象が木であって合流がないのでメモ化再帰にする必要はない
python

```
def solve(N, edges):
    def visit(parent, self):
        if parent != 0 and len(edges[self]) == 1:
            # self is leaf
            return (1, 2)  # white, total

        black = 1
        white = 1
        for child in edges[self]:
            if child == parent:
                continue
            w, t = visit(self, child)
            black *= w
            black %= MOD
            white *= t
            white %= MOD
        ret = (white, white + black)
        return ret

    return visit(0, 1)[1] % MOD
```

PyPy TLE [https://atcoder.jp/contests/dp/submissions/15078877](https://atcoder.jp/contests/dp/submissions/15078877)

Cython
- [https://atcoder.jp/contests/dp/submissions/15078970](https://atcoder.jp/contests/dp/submissions/15078970)
