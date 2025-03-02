
[[アイバーソンの記法]]  [[Iverson bracket]]
![image](https://gyazo.com/f34157fc1cb1fb44299121220725502a/thumb/1000)
- [アイバーソンの記法 - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%82%A4%E3%83%90%E3%83%BC%E3%82%BD%E3%83%B3%E3%81%AE%E8%A8%98%E6%B3%95)
- $\sum_{x:0<x<N} f(x) = \sum_x f(x)[0<x<N]$
- 個人的にはクロネッカーのデルタとか指示関数とかは読みづらくなるので嫌いだったのだが、この記法だとあんまり読みづらくならないからいいなと思った
    - TrueもFalseも値が0でない時はまとめるよりもバラして書いた方が読みやすいと思う(下記B)
        - A: $(x < 0 ? -1 : 1)$
        - B: $-1[x<0] + 1[x\ge0]$
        - C: $1 -2[x<0]$
        - D: $-1\delta_{x<0} + 1 \delta_{x\ge0}$
        - E: $1 - 2\delta_{x<0}$
- [Two notes on notation - Donald E. Knuth](https://arxiv.org/abs/math/9205211)
    - $[k \,\,\mathrm{even}] [k \,\,\mathrm{odd}] [k \,\,\mathrm{prime}] [k \,\, \mathrm{divedes} \,\,  n]  $  などの書き方も。

[[クロネッカーのデルタ]]
![image](https://gyazo.com/b0463982ecb09c045acdd774d66c27d5/thumb/1000)
- [クロネッカーのデルタ - Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%AF%E3%83%AD%E3%83%8D%E3%83%83%E3%82%AB%E3%83%BC%E3%81%AE%E3%83%87%E3%83%AB%E3%82%BF)

[[指示関数]]
![image](https://gyazo.com/86ae63fcd61a851bd0318e7e2afc1615/thumb/1000)
- [指示関数 - Wikipedia](https://ja.wikipedia.org/wiki/%E6%8C%87%E7%A4%BA%E9%96%A2%E6%95%B0)
