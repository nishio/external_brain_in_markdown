---
title: "EVoC"
---

[[Polis 2.0]]の中で使われているクラスタリングアルゴリズム
- [https://github.com/TutteInstitute/evoc](https://github.com/TutteInstitute/evoc)
- [[UMAP]]と[[HDBSCAN]]の良いところを残して必要ないところを削った的なことが書いてある
- UMAPとHDBSCANを使うのではなく、思想をもとに自前で実装して高速にしている、こういうの好きw
- HDBSCAN由来の「ノイズ点を捨てる」特徴はもちろん引き継いでる
- 以前HDBSCANを使った時は遅いから外そうということになったか、これを使うことで高速になってやりたかったことができるかもしれない
- 広聴AIのアルゴリズムにプラグインが可能になったら僕がやりたいことの最有力候補
- > EVoC does not produce a 2D layout, so you can't extract it.
    - [https://github.com/TutteInstitute/evoc/issues/19?utm_source=chatgpt.com](https://github.com/TutteInstitute/evoc/issues/19?utm_source=chatgpt.com)
- 詳細解説
    - [https://gist.github.com/nishio/ca7fe0904f81b6ab7933c0e40855e322](https://gist.github.com/nishio/ca7fe0904f81b6ab7933c0e40855e322)
