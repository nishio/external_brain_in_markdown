
![image](https://gyazo.com/3ece755849cf9ae710151121e2a7c36a/thumb/1000)

Highway Network
- [https://arxiv.org/pdf/1505.00387.pdf](https://arxiv.org/pdf/1505.00387.pdf)
- 非線型変換F, Gがあって
- $z = F(y) \otimes G(y) + y \otimes (1 - G(y))$
    - Gは0〜1の範囲の値を返すようにしてあって、yを素通しするか(0)、F(y)だけを使うか(1)の間の混合係数になる

Residual Block
- [[ResNet]]の構成ブロック
- Highway Networkとの比較だと
- $z = F(y) + y$
- 混合比率が1:1に固定されている状態
    - 「混ぜる」っていうと0.5と0.5になっているような誤解を招くから良くない表現か
    - 残余(Residual)という名前の通りFがz-yを学習する: $F(y) = z - y$
