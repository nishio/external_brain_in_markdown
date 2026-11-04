---
title: "Weight-space programming"
---

> [rikiyatakehi](https://x.com/rikiyatakehi/status/2117313742891327994) We asked GPT-6 Astra to edit Qwen3.5-0.8B weights to improve math.
>  It directly changed only 0.016% of weights, fixing 0.8B's reasoning loops & improving math up to 6x and even instruction following 3x, without gradients or training.
>  We call this Weight-Space Programming: frontier LLMs can now natively read/write neural network weights! 🧵
- [Sparks of Weight-Space Programming: LLMs can natively read & write neural network weights](https://rikiyat.github.io/blog/weight-space-programming/)

> [AlexKrentsel](https://x.com/AlexKrentsel/status/2117376683724660898) i've reproduced the results from the MIT blog post today on weight-space programming. but one additional result i have to add: this is a new, step-change emerging capability that's appeared in just the latest set of models.
>  ![image](https://scrapbox.io/files/6ae9d3d22770911e72d7d5aa.png)

> [nishio](https://x.com/nishio/status/2117346729867817016) これはマジか、最優先で追試することにした。
> [nishio](https://x.com/nishio/status/2117438978181996632) 寝てる間に雑に検証させといたんだけど、Opus5.5でもゲームの自己対戦で学習しているニューラルネットの重みを編集して問題行動を減らすことができているな
>  ![image](https://pbs.twimg.com/media/HWKnBmxaQAEJNGo?format=png&name=medium#.png)
> [nishio](https://x.com/nishio/status/2117439234625925425) 何が問題行動であるとして修正の対象にするか決めるとこまで寝てる間にOpusが決めて実行している

> [nishio](https://x.com/nishio/status/2117451661581111348) どういうことが可能でどういうことが難しいのかとか、Qwenの場合は何が特定された悪い振る舞いであったのかとか色々わかってきたので、「もちろん万能ではないが、できると思ってなかったことが意外とできるってわかったので可能性が広がった」くらいのトーンにしておきます
- Qwenの数学能力に関しては、そもそも試行中にループに陥ってしまってthinking budgetを使い切って答えが出せないという「愚かな」振る舞いをしていて、weightの編集によってその振る舞いの傾向を減らしたので性能が上がった
    - 賢く振る舞っているものをさらに賢くすることができているわけではない
- ごく少数の重みの修正で大きな挙動の変化が起きるのは、[[abliteration]]がたかだか1次元でも効果あるのと同じニュアンス
- 僕の上記の検証でも、失敗行動が起きてる時に発火しているニューロンを特定してその重みをいじることでその振る舞いを止めているだけ
    - 結果としてトレードオフの関係にある「4つ目の赤をとって負ける確率」は上昇している
    - 「トレードオフの関係にあるものたちの巨大なネットワークをバランスさせながら改善すること」は結局フルネットワークのファインチューニングと同程度に大変
        - 現実世界の一部の問題に関しては「トレードオフの関係」のネットワークを小さく限定しても価値を出せることがあるってこと

Weight-space programmingについて
> [nishio](https://x.com/nishio/status/2117442726585409851) つまり「コンピュータが実行可能な処理」のうち「既存のプログラミング言語で直接書ける処理」が占める領域は狭くて「重みによって表現してそれを学習によって調整することで表現できる処理」はもっと広いが、調整のコストが高かった。しかし2026年後半のAIはこの「重み」を直接編集できる
> [nishio](https://x.com/nishio/status/2117443733889352097) これは限られたコストで実現できる「処理」の範囲を広げるし、その広げられた領域は目下人間があまり読む能力を獲得できてない「重み」の形になっている。
> [nishio](https://x.com/nishio/status/2117443915490177181) AIの生成したコードを読むとか読まないとか議論している人たちがいるが、ほとんどの人がコンパイラの出す機械語も既存の機械学習の重みも読まない。今後多様な処理が重みの形で表現されるようになると、読まないものが増えていくだろうな。

現状のSNSは過度な期待の盛り上がりがあるけど、それを廃してもまあ有用性はあるかなという感じ
- ブラウザの上で動く業務内容特化のLLMが再学習しなくてもOpus5.5でなら直接重み編集してカスタマイズできるわけなので
