---
title: "PositionRank"
---

PositionRank: An Unsupervised Approach to [[Keyphrase Extraction]] from Scholarly Documents
- [[キーフレーズ抽出]] 2017
- [http://people.cs.ksu.edu/~ccaragea/papers/acl17.pdf](http://people.cs.ksu.edu/~ccaragea/papers/acl17.pdf)

単語の隣接関係をグラフにして[[PageRank]]を計算する
通常のPageRankでは等確率のbiasをかけるが、この手法は等確率ではなく単語の出現位置の逆数で重み付けをする
そのことによって従来のPageRankを用いた手法より改善した

名詞と形容詞以外をまず捨てた上で、`(adjective)*(noun)+`の形の最大三単語までの連続をキーフレーズとして抽出する。

Window sizeの影響は少ないとの主張だが、上記の形に限定しているとWindow size > 1 であることが機能するチャンスがとても限られるのではないか。

PageRankをキーワード抽出に使うことの意義がいまいちよくわからない。実際、シンプルな[[TextRank]]は[[TF-IDF]]に負けている。

実装している人がいた
[PositionRankでarXivの論文からキーフレーズ抽出 - Qiita](https://qiita.com/ymym3412/items/bc3d90e9e1b51959649a)
