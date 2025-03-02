---
title: "Stable Diffusionの画像サイズの影響"
---

サンプリング手法が[[DDIM]]か[[PLMS]]かに関しては多少の差はあるが人の目にはあまりわからない
![image](https://gyazo.com/0ed967f2faddaba3bb4b3868949df758/thumb/1000)![image](https://gyazo.com/aa6d3fed9f7d97b07a877b23ea94c4ac/thumb/1000)

むしろサイズの影響が大きすぎて全く別物
![image](https://gyazo.com/5c593cd3ca14658dd22190e76bffc88d/thumb/1000)
![image](https://gyazo.com/2ae797fdd1a543c059438c06bf86b94f/thumb/1000)
![image](https://gyazo.com/86e6ad3429432b611f572eb83a41845e/thumb/1000)
![image](https://gyazo.com/0ed967f2faddaba3bb4b3868949df758/thumb/1000)
小さくても同じ構図なのなら「小さいサイズで高速にたくさん生成してから、良いものを選んで高解像度化」というアプローチが可能だなと思って試したのだが、全然ダメだった

[[Stable Diffusion]]の[[LDM]]は潜在空間で[[拡散モデル]]をやる
- 小さい画像の空間で拡散モデルをしてから[[超解像]]するアプローチではない
- おそらくそのせいだろう
