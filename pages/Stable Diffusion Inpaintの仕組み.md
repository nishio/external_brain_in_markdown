---
title: "Stable Diffusion Inpaintの仕組み"
---

![image](https://gyazo.com/7bbbd2f36bc287afe03cd0b19e6f9ce9/thumb/1000)
- [[VAE]]

![image](https://gyazo.com/f53be72b72b7a24b54c614b70dc8ef89/thumb/1000)

「マスクしてないところだけを描き直してくれる機能」ってのは一般人向けの雑な説明
- 「マスクされてるところは一切変更しないで、残りの部分だけを境界の辻褄が合うように作る」って仕組みではない
- 拡大してみるとマスクされたベンチの網目模様が変化しているのがわかる
    - ![image](https://gyazo.com/3555cfd5ad7d03a520c5be77bb59ad93/thumb/1000)

- マスクされたところも変わってしまうのは当たり前でlatent spaceにその詳しい情報を保持しておけるだけの次元がないから
- 例えマスクもノイズも皆無だったとしても16分の1の情報量から画像を復元してるので揺らいでしまう
