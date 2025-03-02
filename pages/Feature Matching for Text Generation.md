
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Feature Matchingとは何か？
- [[Salimans+ 2016]]
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Maximum Mean Discrepancyとは何か？

[[GAN]]のGに[[LSTM]]、DとEに[[TextCNN]]を使う
- Eってなんだ？→Encoder

### Soft-argmax approximation
- argmaxは微分可能でないので扱いに難しさがあるが、これをsoftmaxに置き換えても良いのではないか、って提案。
- $W[\arg\max_i x_i] \approx W \mathrm{softmax}(L x_i)$
- ここでLは1000とかの大きなスカラーで、L→∞の極限ではargmaxに一致する。
- 計算の安定性は別途きにする必要がありそう。関連 [[logsumexp]]
- [[Soft-argmax]]

[Adversarial Feature Matching for Text Generation | DL Hacks](https://hacks.deeplearning.jp/adversarial-feature-matching-for-text-generation/)
[DL輪読会 Adversarial Feature Matching for Text Generation](https://www.slideshare.net/DeepLearningJP2016/dladversarial-feature-matching-for-text-generation)
