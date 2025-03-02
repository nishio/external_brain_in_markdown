---
title: "Toward Controlled Generation of Text"
---

ニューラルネットによる文章生成タスク
Generatorは[[LSTM-RNN]]
隠れ変数zはEncoderが出力する確率分布からランダムにサンプリングされる
[[VAE]]:[[変分オートエンコーダ]]
Discriminatorは文章を入力として受け取ってcを作る
青点線は後半で提案する独立制約
赤矢印は変分近似で可能になるバックプロパゲーション
[[GAN]]的構成

![image](https://gyazo.com/a10a9ee3a963b880f7470373c273ddb5/thumb/1000)

学習アルゴリズムは、GeneratorとDiscriminatorを交互に学習させる
![image](https://gyazo.com/c2129280c86d21571c7e765c095b00d9/thumb/1000)

> Zhiting Hu, Zichao Yang, Xiaodan Liang, Ruslan Salakhutdinov, Eric P. Xing
> (Submitted on 2 Mar 2017 (v1), last revised 13 Sep 2018 (this version, v4))
> Generic generation and manipulation of text is challenging and has limited success compared to recent deep generative modeling in visual domain. This paper aims at generating plausible natural language sentences, whose attributes are dynamically controlled by learning disentangled latent representations with designated semantics. We propose a new neural generative model which combines variational auto-encoders and holistic attribute discriminators for effective imposition of semantic structures. With differentiable approximation to discrete text samples, explicit constraints on independent attribute controls, and efficient collaborative learning of generator and discriminators, our model learns highly interpretable representations from even only word annotations, and produces realistic sentences with desired attributes. Quantitative evaluation validates the accuracy of sentence and attribute generation.
