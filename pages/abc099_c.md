---
title: "abc099_c"
---

[https://atcoder.jp/contests/abc099/tasks/abc099_c](https://atcoder.jp/contests/abc099/tasks/abc099_c)
- 1回で引き出せる金額の種数は高々20回程度
- Nから幅優先で探索して間に合うかなぁ
    - もちろん「より短い手段で訪問済み」なら枝刈りするとして。
    - 各頂点最大1回探索待ちリストに入って、入ったものから20件が探索されるか、2×10^6ぐらい
    - ABCのC問題だからそんなに難しくないのでは
- 公式解説
    - 上記の方法で良いかは書かれていない
    - 想定解法はN以下のiについて、それを6と1だけで表現するコストと、残りを9と1だけで表現するコストを求めて最小値を見つけるもの

