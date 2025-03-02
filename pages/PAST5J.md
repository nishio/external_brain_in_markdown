
[J - 長い長い文字列](https://atcoder.jp/contests/past202012-open/tasks/past202012_j)
![image](https://gyazo.com/a30032ca3d2b05fc4156aed0ed48365c/thumb/1000)
- 初回考察
    - 素朴に出力はできない
    - 各繰り返しのブロックのサイズを前計算しておけば、クエリの値を徐々に剰余とっていくことで解決するだろう
    - 考察完了
- 本番実装
    - 落ち着いて実装するべきだったのに混乱してしまう
        - 一つズレのバグを解決してようやくサンプルが通ったのが56分後
        - しかしTLE
        - 繰り返しの単位になる文字列を切り出して使ってたけども、元の文字列のどこから開始するかだけを待てば良いと考える
        - さらに16分使ってまたTLE、それどころかMLEもある
        - どういうことか？！
        - 例えば9がたくさん続いた時に「繰り返しブロックのサイズ」はとても大きな数になる、これを意識せずにそのままやってたのが問題
        - リアルタイムでは「まったく方針が間違ってたということか？」と思って諦めた
            - 一晩寝て起きたら、クエリとして渡される数が10^15以下だと制限されてるので、それを超えた時点で文字列のパース処理を打ち切ってしまって良いと気づいた
- コンテスト後の再実装
    - 数字1の出現は「そこまでの記述が2回繰り返される」という意味
    - 末尾に0がついてると考えると良い。[[番兵]]
    - ブロックは「1個以下のブロック」「0文字以上のアルファベット」「1文字の数字」からなる、と定義できる
    - 混乱の原因の一つ、概念が明確に分かれていないうちに適当な名前をつけてしまい、名前に引きずられて概念の認識が歪む
    - ![image](https://gyazo.com/ce5657a86b818f20d5d59560de74b9ef/thumb/1000)
    - 本番はblockとunitを混同した
    - blocklen(i + 1) = (blocklen(i) + taillen(i + 1)) * repeat(i + 1)
    - パース後の流れ
        - Xを0-originにする
        - これはunit(-1)が繰り返された文字列なのであまりを取る
- AC
python

```
def solve(S, X):
    X -= 1  # 1-origin to 0-origin
    S += "0"
    blocklen = [0]
    unitlen = [0]
    repeat = [0]
    tailstart = [0]
    taillen = [0]
    tlen = 0
    tstart = 0
    for i, c in enumerate(S):
        if c in "0123456789":
            rep = int(c) + 1
            repeat.append(rep)
            tailstart.append(tstart)
            taillen.append(tlen)
            unitlen.append(blocklen[-1] + tlen)
            blocklen.append(unitlen[-1] * rep)
            if blocklen[-1] > X:
                break
            # next tail
            tstart = i + 1
            tlen = 0
        else:
            tlen += 1

    for i in reversed(range(len(blocklen))):
        X %= unitlen[i]
        if X >= blocklen[i - 1]:
            X -= blocklen[i - 1]
            return S[tailstart[i] + X]
```




[PAST #5 J - 長い長い文字列 - えびちゃんの日記](https://rsk0315.hatenablog.com/entry/2020/12/29/162310)
