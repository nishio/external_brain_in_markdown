
[H - コンベア](https://atcoder.jp/contests/past202012-open/tasks/past202012_h)
![image](https://gyazo.com/f0e4b1e3e154ed74f38484fa80a6fd5a/thumb/1000)
- 初回考察
    - 動かせるか判定
    - グラフを構築して、各始点から「ゴールにたどり着けるか」をDFS
    - 頂点数10^6、大丈夫？
    - スタートがたくさん、ゴールは一つ
        - →[[ゴールをスタートにする]]
    - グラフを逆辺で作っておき、ゴールを始点として到達可能頂点を探索する。
        - 各頂点高々4本の辺しか持たないのでO(N)で間に合う
    - 考察完了
- 実装
    - グラフを逆辺で作り、ゴールから再帰呼び出しDFSでたどりつく頂点をマーク
        - [10TLE](https://atcoder.jp/contests/past202012-open/submissions/19032906)
        - コンテスト後に試しにPython3で出してみたら[14TLE](https://atcoder.jp/contests/past202012-open/submissions/19032925)
    - グラフを構築しないで地図データを使って探索
        - コンテスト中は3TLE 1MLEだったとメモされてるが、今出し直してみたら[3TLE](https://atcoder.jp/contests/past202012-open/submissions/19033329)だった、勘違いかな？
        - Python3だと1MLE
    - 再帰呼び出しでの探索をwhileループに書き換え
        - 1TLE
    - 結果出力での文字列結合を減らす
        - 文字列をループの中で結合しないでリストにappendしておき、最後にjoinする
        - AC
- 考察
    - 今回、問題条件から最悪の場合頂点数が10^6になる
    - Pythonで頂点ごとにリストを持つ実装の場合、その構築コスト自体が無視できない
    - 到達可能性チェックを再帰呼び出しDFSで実装したが、[[PyPyの関数呼び出しは遅い]]
    - MLEは何が悪いか…
    - 文字列結合を減らしてないのは単純にうっかりミス
        - 念のためグラフ構築しつつ文字列結合だけ減らしてみたのを提出してみたが、これは9TLEだったから主要因ではない
python

```
def solve(H, W, R, C, world):
    visited = [False] * (WIDTH * HEIGHT)
    stack = {WIDTH * R + C}

    while len(stack) > 0:
        pos = stack.pop()
        visited[pos] = True

        next = pos - 1
        if not visited[next]:
            if world[next] == 1 or world[next] == 2:
                stack.add(next)

        next = pos + 1
        if not visited[next]:
            if world[next] == 1 or world[next] == 3:
                stack.add(next)

        next = pos + WIDTH
        if not visited[next]:
            if world[next] == 1 or world[next] == 4:
                stack.add(next)

        next = pos - WIDTH
        if not visited[next]:
            if world[next] == 1 or world[next] == 5:
                stack.add(next)

    for y in range(ORIGINAL_HEIGHT):
        line = []
        for x in range(ORIGINAL_WIDTH):
            pos = WIDTH + 1 + WIDTH * y + x
            if world[pos] == 0:
                line.append("#")
            elif visited[pos]:
                line.append("o")
            else:
                line.append("x")
        print("".join(line))
```


