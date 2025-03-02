---
title: "nikkei2019_qual_C"
---

[C - Different Strokes](https://atcoder.jp/contests/nikkei2019-qual/tasks/nikkei2019_qual_c)
- ![image](https://gyazo.com/4ed59c16891725e4088f629ba8803ad0/thumb/1000)
- 考えたこと
    - 気にすることが最終的なスコアの差だけなので差D=A-Bについてだけ考える
    - 後手が邪魔しないなら先手はDの大きい方からceil(N/2)個を取りたい
    - 後手は当然邪魔をする。一番先手にとって邪魔なのは最大のD
    - というわけでDの大きい方から交互にとっていったものが正解
- 公式解説
    - ケアレスミス
        - > D=A-B
    - その得点の差はA+Bになる
