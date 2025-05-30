---
title: "Memory Network"
---

[Memory Networks (End-to-End Memory Networks の Chainer 実装)](https://www.slideshare.net/shuyo/memory-networks-endtoend-memory-networks-chainer)
[[LSTM]]との比較

[論文解説 Memory Networks (MemNN) - ディープラーニングブログ](http://deeplearning.hatenablog.com/entry/memory_networks)

old title: 記憶ネットワーク
[[深層学習による自然言語処理]] p.99
[arXiv: Memory Networks](https://arxiv.org/abs/1410.3916)
[[強教師あり記憶ネットワーク]]

記憶の追加: $m_N \leftarrow x$
記憶の取り出し:
$o_1 = \mathrm{argmax}_i S_O(x, m_i)$
$o_2 = \mathrm{argmax}_i S_O((x, m_{o_1}, m_i)$
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この形では$o1\neq o2$が保証されないのでは？
$r = \mathrm{argmax}_{w\in \mathcal{V}} S_R((x, m_{o_1}, m_{o_2}), w)$

SO, SRはそれぞれ
$s(x,y) = \Phi(X)^T \; U^T \; U \; \Phi(y)$
$\Phi$はD次元への埋め込み
このSO, SRの学習に必要な教師データを用意できるかどうかが現実問題としてはシビア

そこでend-to-end memory network
[[end-to-end memory networks]]
