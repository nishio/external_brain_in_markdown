---
title: "end-to-end memory networks"
---

from [[Memory Network]]
end-to-end memory networks
Sukhbaatar, S., Weston, J., & Fergus, R. (2015). End-to-end memory networks. In Advances in neural information processing systems (pp. 2440-2448).
入力文$x_i$は各単語の埋め込み表現の総和で埋め込まれる
$m_i = \sum_j Ax_{ij}$
質問文qも同様に埋め込まれる
$u = \sum_j Bq_j$
N個の各記憶情報のuに対する重要度pは内積のソフトマックス
$p_i = \mathrm{softmax}(u \cdot m_i)$
$o= p \cdot \sum_j Cx_{ij}$
要するに[[ソフト注意機構]]
$\hat{a} = \mathrm{softmax} (W(o+u))$
色々そんな設計でいいのか？と疑問に思うところはあるが、end-to-endで最適化するために、全体を微分可能にしなければならないという制約が厳しいのである。
![image](https://gyazo.com/87e61c10f3997c3f3b7fe412b2b08aea/thumb/1000)

