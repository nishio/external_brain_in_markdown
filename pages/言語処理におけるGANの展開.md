---
title: "言語処理におけるGANの展開"
---

![image](https://gyazo.com/89f4af857610ae486f09b7f2598cd5dd/thumb/1000)
- [Slideshare](https://www.slideshare.net/mamoruk/jsai2018gan4nlp)
- [[小町 守]]
- [[自然言語処理]]における[[GAN]]

画像の生成ではなく文章の生成にGANを使えないか、というところまでは僕も考えたが、どう構成したら良いかがよくわからなかった。このスライドにはよくまとまっているので参考にする。

p.10
GAN を自然言語の系列データ に適用する際の問題点
- 問題1: 系列を扱う場合 Generator の出力が離散値 なので、Discriminator の学習が困難
1. 強化学習（policy gradient）を用いて Generator が確率的な方策とみなして学習
2. Generator の出力を近似して、微分可能な形 にして学習
- 問題2: Discriminator として何を使えばいい？
1. CNN/RNN → より複雑なモデルへ……
2. 何を敵対的サンプルとするか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>問題1の問いの意味がわからない…
- 「離散値なので学習が困難」とはどういうことか？？
- 離散値だからなの？出力の長さが不定だからでは？

p.12
SeqGAN: 系列データのための GAN の古典的論文
- Yu et al. SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient (AAAI 2017)
- ポイント
    - • 系列を扱う場合 Generator の出力が離散値なの で、Discriminator の学習が困難 →強化学習を用いて Generator を学習
    - • Discriminator は完全な系列しか評価できない →モンテカルロ探索を行う
![image](https://gyazo.com/394f2cbcea32a9323ea1a3f673976664/thumb/1000)

- 単語列を「強化学習における行動の連続」と解釈
- ある単語列が出た後の、次の単語の出現確率の分布
    - 自然言語の分野では言語モデルと呼ばれるやつ
    - 強化学習の分野では確率的方策と呼ばれる
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>モンテカルロ探索をなにに使うのかよくわからない
    - 次のスライドを見ると、強化学習の枠組みで捉えるのはMUSTではなさそうだ

p.16
- textGAN: 強化学習を用いずに 言語生成のための GAN の学習
- Zhang et al. [[Feature Matching for Text Generation]] (ICML 2017; textGAN)
- ポイント
    - • 強化学習ではなく [[Soft-argmax]] により微分可能 にして Discriminator を学習
    - • 離散的な単語ではなく潜在空間で最適化を行う

p.17
p.18
p.19
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>わからない

p.20 SeqGANより良いらしい

p.22 MaskGAN
- 系列の穴埋めができる
- [[Teacher-Forcing]]

- Encoderを一部マスクしてそこを埋めさせる
    - ある種の[[Dropout]]かなぁ
