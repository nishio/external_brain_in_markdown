---
title: "Grokking"
---

> [hillbig](https://twitter.com/hillbig/status/1762624222260846993/history) NNで訓練誤差が0になった後も学習を続けると汎化性能が改善されるGrokkingは、非線形領域（動画中の黒線）が分類面に移動する相転移がおき、サンプル周辺領域が線形化される（敵対的摂動にも頑健になる）現象がおこるため。動画による可視化がすごい [https://arxiv.org/abs/2402.15555youtube.com](https://arxiv.org/abs/2402.15555youtube.com)
>  Grokking Visualized for MLP trained on MNIST
>  Supplementary Video for paper:Grokking Happens All the Time and Here is Whybit.ly/grok-adversarialWe train a 4 layer MLP with 256 width, on 1000 training sam...

なるほど
before
![image](https://gyazo.com/ca9d58db23682619d2e208ea46d205ba/thumb/1000)
after
![image](https://gyazo.com/6e808ae2a6b3f3f9188e25d1b2d3b6a0/thumb/1000)

