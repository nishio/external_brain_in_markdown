---
title: "abc120_d"
---

[https://atcoder.jp/contests/abc120/tasks/abc120_d](https://atcoder.jp/contests/abc120/tasks/abc120_d)
- 考えたこと
    - 行き来できないペアの数を数える
    - [[余事象を引く]]
        - 行き来できる島=連結
        - 連結成分のサイズがわかれば[[三角数]]
    - [[時間軸反転]]して考えると1本ずつ辺を増やして行く構図
    - [[UnionFind]]で連結成分を求めたらいい？
    - 連結成分のサイズを求める処理で各頂点のrootを確かめると間に合わないのでroot→sizeの形で持つ必要がある
- 公式解説
    - OK
    - UnionFindでsizeがO(1)と書いてるけど、そういう実装であるとは限らないのでは？
