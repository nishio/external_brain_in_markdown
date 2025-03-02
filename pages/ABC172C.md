
長さ20万の数列が二つ与えられる(A,B)。Aの先頭i個とBの先頭j個を足した時に、与えられた数Kを超えないような、最大のi+jを答えよ、という問題。

コンテスト中の思考
- 問題文では「数列の先頭から一つずつ取り…」と書いてあるが、小さい方を取ればOKか？
    - 反例が見つかった
        - ![image](https://gyazo.com/e4691f605cbf81dd6aa75503417e1b7f/thumb/1000)
        - 6以下であることが求められてるとして、正解は3,1,1,1で6にすることなのに、先に2を取ってしまうと2,3,1になってしまう。これは最適解ではない。
- 取る順番は関係ない
    - Aを取ってからBを取っても、その逆でも、やる計算は「足し合わせ」なので同じ値になる
    - [[問題文の順にやらない]]
- i+jが小さい方から順にチェックしよう
![image](https://gyazo.com/6fc6007792d68986558252292a22d018/thumb/1000)

コンテスト後
- 上のやり方でダメな理由
    - 数列が全部1で、Kが50万だとすると、正方形を全部チェックすることになる
    - これには400億回の比較が必要

正解のやり方
![image](https://gyazo.com/f84276e6336eb5180864965deca093bb/thumb/1000)
- 右上隅から初める
- NGであるなら右に進む
    - Kを超えててもっと減らす必要があるから
- OKなら下に進む
    - そこより右はOKだが、i+jが小さいからチェックする意味がない
    - 右端からやる必要はない
        - NGの下はNGだから(既に超えてるなら、増やしても超えてる)
- 多くてもN+M回の比較で各行で一番右にあるOKマスを確実に踏むことができる

python

```
def solve(N, M, K, sA, sB):
    max_can_read = 0
    last_max_j = M
    for i in range(N + 1):
        j = last_max_j
        while j >= 0:
            if sA[i] + sB[j] <= K:
                if max_can_read < i + j:
                    max_can_read = i + j
                last_max_j = j
                break
            j -= 1

    print(max_can_read)
```

AC [https://atcoder.jp/contests/abc172/submissions/14782042](https://atcoder.jp/contests/abc172/submissions/14782042)

[[atcoder]]
