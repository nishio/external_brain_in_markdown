---
title: "クラスタ解説の埋め込みベクトルをconcatしてUMAP"
---

[[広聴AI]]
from [https://docs.google.com/document/d/1plggszRTxEEYUcZuCLiHkPrBsMtxr3RQpctKtZe5y4M/edit?tab=t.0#heading=h.xqz9vh6im1kw](https://docs.google.com/document/d/1plggszRTxEEYUcZuCLiHkPrBsMtxr3RQpctKtZe5y4M/edit?tab=t.0#heading=h.xqz9vh6im1kw)
先週のクラスタリング精度アップの議論に関して
- まず精度の尺度を作らないと議論にならない
- 過去の実験レポートを発掘した [https://github.com/nishio/broadlistening-research/blob/main/publish/2025-02-11-02-NISHIO.md](https://github.com/nishio/broadlistening-research/blob/main/publish/2025-02-11-02-NISHIO.md)
- 基本的にはUMAPしてからクラスタリングしてるのをやめるといいと思う
    - 高次元空間上でHDBSCANするだけで大部分の問題は解決するはず
    - ただし高次元空間を人間は観察できないので散布図は出せない
- An Empirical Configuration Study of a Common Document Clustering Pipeline
    - UMAPで2次元に落としてからクラスタリングすることは精度を落とすという研究
- 分析のための散布図を直接市民に提示するのではなく、分析結果をわかりやすく伝えるための図を生成する(クラスタリングした後で散布図を作るなど)というアプローチもあり
    - 高次元でクラスタリングしてからUMAPした場合、クラスタが重なってしまう可能性が大いにある、実用的な見た目になるかどうかは実験してみるといいと思う
    - 分かれない場合、たとえば個別意見の埋め込みベクトルにクラスタ解説の埋め込みベクトルをconcatしてUMAPするなどの方法で分離した描画が可能なはず

2025-10-20
[[高次元空間でクラスタリングしてからUMAP]]に対して
クラスタ1に$(a,  0, 0, \cdots)$をconcatする
![image](https://gyazo.com/a2092bb3b3c3d51cd12fc22c4af265f6/thumb/1000)
- できた
    - a=10
    - クラスタの情報が圧倒的になっている
![image](https://gyazo.com/38302b468d7902bfdb1820a61fdf8b41/thumb/1000)
- a=1でもたいして変わらんな
    - 「明瞭分離している」となったらUMAPが明瞭に離して描画するからか

![image](https://gyazo.com/9b48084dff540108755f6bfbb11a38f8/thumb/1000)
- a=0.5にしたらこう
    - 明瞭分離でなくなると他のクラスタに巻き込まれるものが出てきて乱れるだけ
    - 全体的な「綺麗に分離されてる」感は変わらない
- 定数aではなくクラスタの説明のembeddingをconcatする形ならもう少し配置に意味は出てくるだろうけど、その場合でも2次元的に見た配置はこの0.5のオフセットの場合と同じようにユーザから見て「不可解な飛地」ができるだけだろう

想像の確認のためにa=0.3
- ![image](https://gyazo.com/9c3bee03dd3ffd22957c5cbbb1d7f968/thumb/1000)
- やっぱそうなるよねぇ
    - [[高次元空間でクラスタリングしてからUMAP]]に近づいていくだけ

2025-10-21
[[Supervised UMAP]]の結果を書いてなかった。結局クラスタの間の距離を増やすという数学的な扱いがこの手法とほぼ同じだから、結果も似たようなものになる感じ

![image](https://gyazo.com/2ffb16ae682de1329841142c118e37ab/thumb/1000)

2025-10-22
いっそ[[AffinityBubble]]路線にする手もあるか…
