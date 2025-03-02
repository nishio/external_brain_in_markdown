
[M-SOLUTIONS プロコンオープン 2020 - AtCoder](https://atcoder.jp/contests/m-solutions2020)
- 4連休でのんびりしてたらすっぽかしたので事後的に解いた

[B - Magic 2](https://atcoder.jp/contests/m-solutions2020/tasks/m_solutions2020_b)
- 全探索できるサイズだなとは思ったが、最短手数を求めて足りてるかどうかを判断した。公式解説と同じ。
python

```
def solve(A, B, C, K):
    while A >= B:
        K -= 1
        B *= 2
    while B >= C:
        K -= 1
        C *= 2
    if K >= 0:
        return "Yes"
    return "No"
```


[C - Marks](https://atcoder.jp/contests/m-solutions2020/tasks/m_solutions2020_c)
- 複数の数の移動ウィンドウでの積を比較する問題
- 最大10^9の値を20万個掛け算することになるので早々に「掛け算はしない」という方針
- ウィンドウの前後で比較すれば良いだけ
python

```
def solve(N, K, AS):
    for i in range(K, N):
        if AS[i - K] < AS[i]:
            print("Yes")
        else:
            print("No")
```


[D - Road to Millionaire](https://atcoder.jp/contests/m-solutions2020/tasks/m_solutions2020_d)
- なんらかの探索が必要なのかどうなのか、を考えるためにまずは末尾から2日、3日の範囲で行動を考えた
- ![image](https://gyazo.com/df02ad9d7fe5c167973c1544998e93ea/thumb/1000)
- 結論、要するに単調増加の始まるところで全力で買い、単調非減少の終わるところで全力で売れば良い、と考えた
    - 大きな上昇トレンドの中に窪みがある場合でも、窪みの直前で売って窪みの底で買えばより良い結果になるから。
    - それを実装したら「明日値上がりするなら買う、明日値下がりするなら売る」というシンプルな行動ルールに帰着した
python

```
def solve(N, XS):
    cash = 1000
    stock = 0
    for i in range(N - 1):
        price = XS[i]
        if cash >= price:
            if XS[i + 1] > price:
                # buy
                s = cash // price
                stock += s
                cash -= s * price
                continue
        if stock > 0:
            if XS[i + 1] < price:
                # sell
                cash += stock * price
                stock = 0
    # last day
    cash += stock * XS[-1]
    return cash
```


[E - M's Solution](https://atcoder.jp/contests/m-solutions2020/tasks/m_solutions2020_e)
- 時間内に解けなかった。
    - 正しい解法にたどり着いたと自信満々で実装して上手くいかなかった
        - サンプルケースでは全部うまくいったのにサブミットするとダメなパターン
        - 解説みたら解法が正しくなかったので、今度改めて解く
    - ここでは時間内に考えたことを書く
- ![image](https://gyazo.com/4143c57fa23ff42b8189ae010fbfd7a7/thumb/1000)
    - まず考えたのはこれは1本ずつ足していけば良い問題なのかどうか
        - よく見たらサンプルでそうではないケースが紹介されてた
    - 次に考えたこと、線の選択肢はいくつあるか
        - 都市の上を通ってない線に関しては、それをより人数の多い側にずらすことでスコアが改善する
        - 人数がイコールである場合にも悪化はしない
        - なので都市の上を通る線だけを考えて良い
        - 線の追加順は関係ない
            - なのでスコアは線選択肢の部分集合を定義域とする関数
            - 距離は、新しく追加された線への距離とのminを取ることで更新できる
            - 集合を定義域とし、距離を値とする動的計画法
        - 都市が15個なので線は最大30、部分集合を整数にパックできるサイズだ→　[[bitDP]]
- この方針のダメだった点
    - 計算量の見積もりが甘い、2^30はおよそ10^10なので、数秒で計算するのは無理、さらに削減する必要があった
        - 本数オーバーで打ち切ってるから十分小さいかなぁと思ったのだが…
        - comb(30, 15)は1.6 * 10^8
    - 3^15だと 1.4 * 10^7ぐらいになる(この計算は暗算ではできなかった)
        - ある都市を線が通った場合(wlog南北に)、その都市は以降の線の置き方によらず距離0なので東西に並ぶ都市がない限り東西の線は通らない
    - 解説ではこれに加えてN^2をNに削減する議論をしている
        - 「距離は、新しく追加された線への距離とのminを取ることで更新できる」を使えばNなのではと思う
- 追記: そもそも`[None] * (1 << 30)`はAtCoder環境ではMemoryErrorでREになる(MLEではない)
    - 空間計算量の見積もりが甘々だった
    - サイズ30の集合の部分集合を考えてはいけない
    - 南北線と東西線を別々に考えて2^15+2^15にするべきだった
    - [[半分全列挙]]っぽい発想だ
