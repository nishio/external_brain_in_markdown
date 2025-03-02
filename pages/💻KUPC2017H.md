
[H - Make a Potion](https://atcoder.jp/contests/kupc2017/tasks/kupc2017_h)
![image](https://gyazo.com/f2dc4a6aa7acee93e06792643d101b59/thumb/1000)
- 考えたこと
    - 最小カットに帰着できることは既知
    - 選択肢が二択ではないが、[[最小カットで3以上の選択肢]]でよい
    - しかしvの範囲が10^6まであるので全部頂点にすると辛い
    - 制約に関係する頂点だけを選ぶ[[座標圧縮]]が必要か
        - 効力がプラスなら、制約ギリギリa-1まで入れた方が得
        - 効力がマイナスなら制約ギリギリbで止めるのが得
- 実装
    - ![image](https://gyazo.com/9691ec6d4f71c67caf7c82d036afbba4/thumb/1000)
    - ![image](https://gyazo.com/8ca69974b4a52090025c6d4f0c93111b/thumb/1000)

    - 頂点数が不規則なのが実装めんどくさい…

