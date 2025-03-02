---
title: "フレーズベースTF-IDF: 名詞句解析の応用"
---

- [[フレーズベースTF-IDF]]: [[名詞句解析]]の応用
    - [[tf-idf]]
    - [[キーフレーズ抽出]]
    - [[村脇 有吾]]
    - 論文抄録	文書中の重要語の認識は様々な応用の基礎となるタスクである．そうした重要語は，しばしば単語ではなく，単語列からなる．しかし，教師なし手法における state-of-the-art は，単語 TF-IDF の総和によるスコア付けであり，単語列の意味的まとまりを認識しない．そこで，本稿では，名詞句の内部構造解析を応用し，複数の単語からなるフレーズに対して直接 TF-IDF を算出する手法を提案するとともに，その振る舞いを調べる．

- [[Conundrums in Unsupervised Keyphrase Extraction]]は[[TextRank]]などの手法よりも単語ベース[[TF-IDF]]が強いことを示した
- [[単語ベースTF-IDF]]はフレーズのスコアを構成単語のTF-IDFの和と定義する
    - それに加えて最長名詞句に限定するというヒューリスティクスが無意識に使用されている
    - これによって[[文法性]]の問題を回避している

- unithood
    - “the degree of strength or stability of syntagmatic combinations or collocations”
        - 単語の連なりがひとかたまりのものとして機能している度合い
- termhood
    - “the degree that a linguistic unit is related to (or more straightforwardly, represents) domain-specific concepts”
        - 単語の連なりが特定の概念と結びついている度合い
- 単語ベースTF-IDFは
    - > $\mathrm{tfidfW}(w) = \mathrm{tf}(w) \times log(D/D_w)$
        - where tfは文章中の単語wiの出現頻度、Dは全ての文章数、$D_{w_i}$は単語wiを含む文章の数
    - > $\mathrm{term}(p) = \sum_{w \in p} \mathrm{tfidfW}(w)$
        - p: phrase
    - > $\mathrm{unit}(p) = (p\in\mathrm{longest(doc)) ? 1 : 0}$
        - longestは最長名詞句
    - > $\mathrm{tfidf(p)} = \mathrm{unit}(p) \times \mathrm{term}(p)$
- unitの定義について、最長名詞句であるかどうかだけを使っている。
    - 仮に最長名詞句の部分単語列も全て含めた場合
        - > $\mathrm{unit}(p) = (p\in\mathrm{all(doc)) ? 1 : 0}$
        - Recallの上界をあげる効果があるが、全体的には精度を悪化させた
        - これはつまり、適切でない部分名詞句に対してもunit = 1となっているのがよくない、と考える
        - そこで部分名詞句に対して適切なスコアをつける

このアプローチで、長い文章に対しては精度が向上する
短い文章に対しては向上しない

[https://ipsj.ixsq.nii.ac.jp/ej/?action=repository_action_common_download&item_id=95866&item_no=1&attribute_id=1&file_no=1](https://ipsj.ixsq.nii.ac.jp/ej/?action=repository_action_common_download&item_id=95866&item_no=1&attribute_id=1&file_no=1)
