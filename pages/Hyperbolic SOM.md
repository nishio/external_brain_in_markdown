---
title: "Hyperbolic SOM"
---

[[Hyperbolic Self-Organizing Maps for Semantic Navigation]]
[Hyperbolic Self-Organizing Maps for Semantic Navigation](https://papers.nips.cc/paper_files/paper/2001/hash/093b60fd0557804c8ba0cbf1453da22f-Abstract.html)
<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>
上記の論文（Ontrupらの研究）は、文書集合の「[[意味空間]]」へナビゲートするためのHyperbolic SOMを提案している。当時は主に[[テキストマイニング]]や[[カテゴリ分け]]に応用し、[[ユークリッド空間]]上の[[SOM]]と比較して階層的構造の自然なマッピングや視覚化（双曲空間による「[[魚眼的]]」な拡大表示）が可能な点が強調されている。量子化誤差やクラスタ純度で標準的なSOMと同等以上の性能を示し、さらに新規トピック検出や文書間類似性の理解を容易にしている。

現代のUMAPやt-SNEは高速かつ高次元データの構造を局所的によく捉えるが、必ずしも階層的あるいは木状構造を明示的に扱わない。一方、Hyperbolic SOMは、双曲幾何空間の性質を利用して[[階層的データ]]・[[ツリー状データ]]をより自然にマッピングできる点に独自の強みがある。よって、現代の非線形次元圧縮手法が主流の状況でも、双曲空間を活用したSOMは、特に階層的関係性を重視するタスクで依然として有用な位置付けを占め得る。
