
![image](https://gyazo.com/c34c56dd50d7869ec0a4520a8a9c960c/thumb/1000)

[E - MUL](https://atcoder.jp/contests/arc085/tasks/arc085_c)
![image](https://gyazo.com/cb827e1c07c6b065c57300c21a9293d2/thumb/1000)
- 考えたこと
    - 最小カット絡みであることは既知
    - 割る割らないの二択なのでカットの問題
    - Nは100
    - ある値を選ぶとその倍数はすべて割らなければならない
        - 無限コスト辺
    - 割らなかった宝石に報酬がある
        - 報酬が辺コストだと最大カットになってしまう
        - 割った宝石に「報酬得られない」が発生すると考える
        - 「得られない報酬」を最小化する
        - ![image](https://gyazo.com/85f7ba7eefecb277f4cd69b70eda563d/thumb/1000)
    - 報酬が全部正なら「一つも割らない」が自明な解になる
        - 負の辺がある
        - どう扱うか？
        - 単純にオフセットすれば良いはずだが意味合いは？
        - ![image](https://gyazo.com/b418f3fa2aaa035c2542326b0866c467/thumb/1000)
        - 辺の値は「割らなかった時の利益」=「割った時の損失」
            - 損失を最小化する
        - 割った時の損失が負のものがある
        - まてよ？これですべて正になったらやはりSの右で切られてしまうのでは…
- 公式解説
    - 割った時の損失が負=割ると得=割らないとコスト
        - ![image](https://gyazo.com/3adfceb0bb32bfa1e60a3b9cb7cc1411/thumb/1000)
        - 選ぶ数と割られる宝石を分ける必要はなかった
            - 「xが割られていて、xの倍数が割られてないとペナルティ」でよかった
- 実装
    - 最小カットを求めた後、どうやって求める値にするのか
        - カットを最小化することでスコアが最大化されるのでなんらかのオフセットから引くことになる
        - そのオフセットはサンプルデータを眺めたら「正である価格の和」だったけど、これはどういう理屈？
        - ![image](https://gyazo.com/ce05e85b83185144a9bd870534e1713b/thumb/1000)
        - まず基本は「全部割らなかった時に得られる報酬は価格の和」「割ることによって損失が発生する、その損失は価格とイコール」である(左図)
        - これが大前提としてあった上で「負の辺があると計算の都合が悪いから消したい」が来る。
        - 2の頂点は塗られるか塗られないかの二択なのでそのどちらでも+10されるようにする(右図)
        - 同じ塗りで、左図より10多いコストになる
        - なのでオフセットも10増やす
    - AC
python

```
def main():
    INF = 9223372036854775807
    N = int(input())
    AS = list(map(int, input().split()))
    offset = sum(max(0, x) for x in AS)
    d = Dinic(N + 2)
    start = N
    goal = N + 1
    for i in range(N):
        c = AS[i] 
        if c > 0:
            d.add_edge(i, goal, c)
        else:
            d.add_edge(start, i, -c)
        n = i + 1
        x = 2 * n
        while x <= N:
            d.add_edge(i, x - 1, INF)
            x += n

    print(offset - d.max_flow(start, goal))
```


