---
title: "arc103_c"
---

[E - Tr/ee](https://atcoder.jp/contests/arc103/tasks/arc103_c)
![image](https://gyazo.com/83c5876ac46283a866b2c1c3e8a07dfe/thumb/1000)
- 考えたこと
    - どのように辺を取り除いてもサイズ1の連結成分が作れないとき、端から2番目の頂点の位数は3以上
    - サイズxが作れる時サイズN-x-1も作れる
    - サイズN-1が作れない時、位数1の点があってはいけない
        - 条件を再確認、任意のグラフではなく木であるから、これはありえない
    - [[doing]]
