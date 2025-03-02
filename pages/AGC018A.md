
[A - Getting Difference](https://atcoder.jp/contests/agc018/tasks/agc018_a)
- ![image](https://gyazo.com/783c32fab84daa98daab8903533862f0/thumb/1000)

- 考えたこと
    - 全部が偶数の時に1を作ることはできない
    - 最大公約数がnのペアがあればnは作れる
    - 使ったボールも戻されるので、改めて最大の数mからnを引いていけばm以下のnの倍数は全部作れる
        - このmがnの倍数でないケースがある
        - nが1でないなら、mod nの余りごとに最大のボールを探せばよい
- 公式解説
    - これは間違い
        - > このmがnの倍数でないケースがある
        - だって公約数を求めてるからね
    - 方針はOK
