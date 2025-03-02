
[C - GCD on Blackboard](https://atcoder.jp/contests/abc125/tasks/abc125_c)
- ![image](https://gyazo.com/be7a37e747fc2d81355ee27815fa105a/thumb/1000)
- 考えたこと
    - 1つ取り除いた残りのgcdが1だったらどうあがいても1だよね
        - gcdが引数より大きくなることはないからね
    - つまり「1つ取り除いたgcdの最大値を求めよ」ってこと
    - これは[[一つ除き積]]だね
        - [[左右から累積積]]でOK
- 公式解説
    - 同じ方針
    - 番兵として0を使ってる
    - $\gcd(0, X) = \gcd(X, 0) = X$
    - Python標準のgcdもこの挙動
