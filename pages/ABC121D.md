
[D - XOR World](https://atcoder.jp/contests/abc121/tasks/abc121_d)
- ![image](https://gyazo.com/50b60f8288036da81264d8bbcaa20095/thumb/1000)
- 考えたこと
    - 各ビットごとに考えると、2べきの剰余で区間内の1の数がわかるよね
- 公式解説
    - それは対数オーダー解
    - 下記に気づくと定数オーダー
    - $f(A, B) = f(0, A - 1) \oplus f(0, B)$
        - [[任意の区間は0からの区間の差]]
    - $2n \oplus (2n+1) = 1$
        - [[偶数と次の奇数のXORは1]]
