---
title: "ABC006C"
---

[C - スフィンクスのなぞなぞ](https://atcoder.jp/contests/abc006/tasks/abc006_3)
- ![image](https://gyazo.com/2f6b59dcf7787876c9b5f7e08d21cb47/thumb/1000)
- 考えたこと
    - 全員2だとして、余った数を+1もしくは+2を最大N個組み合わせて作る問題
    - 素朴に二重にループすると間に合わない
    - 余りがN以下ならその数の1を出せば良い
    - 余りがNを超えるなら全員3にして、その余を4に割り振ればいい
    - 定数オーダー
- 公式解説
    - なんだか全然違う話をしてるな
        - 一つ決めれば鶴亀算になるから1つについてだけ全探索、とか、老人は0/1だとわかるから残りを全探索するとか
    - 探索しなくても上記の解法でACする
python

```
def solve(N, M):
    IMPOSSIBLE = (-1, -1, -1)
    x = M - 2 * N
    if x < 0:
        return IMPOSSIBLE
    if x <= N:
        return (N - x, x, 0)
    x -= N
    if x <= N:
        return (0, N - x, x)
    return IMPOSSIBLE
```


[[帰着訓練]]
[[公式より小オーダー]]
[[ABC006]]
