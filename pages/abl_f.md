---
title: "abl_f"
---

[F - Heights and Pairs](https://atcoder.jp/contests/abl/tasks/abl_f)
- ![image](https://gyazo.com/a6ccf80048638b04d410f8a8df2b7275/thumb/1000)
- 考えたこと
    - 「どのペアも高さが同じでない」の[[余事象]]は「どれかのペアで高さが同じ」
    - それは「1つのペアで…」「2つのペアで…」の組み合わせ
    - [[包除原理]]
    - まず高さの[[頻度表]]を作るんだろうな
    - ペアの取り方は対象であるので状態を圧縮できる
    - 2人、3人、4人、とペアがあった時に「ペアが1個ある組み合わせ」はいくつなのか？
    - これは式変形ではなくDPで求めるのかもな？
    - ペアの取り方に順序は関係ないので、こちらで順序を導入して良い
    - 与えられた頻度表Xの先頭i個でjペア作る場合の数でDPかな
    - 4人以上いると、一度に2ペアできる可能性がある
        - 4C2×2C2÷2!
    - Nが10万近くなるのか…
- 公式解説なし
- 解説
    - [https://betrue12.hateblo.jp/entry/2020/09/27/043205](https://betrue12.hateblo.jp/entry/2020/09/27/043205)
    - [https://tiramistercp.hatenablog.com/entry/abl-f](https://tiramistercp.hatenablog.com/entry/abl-f)
    - 「包除原理だ」OK
    - 「頻度表を作る」OK
    - 「サイズ4以上の集合からkペア取る場合の数」OK
    - 「DPかな？」いいえ、[[畳み込み]]です
    - [[繰り返し畳み込み]]をする時は順序を工夫する必要がある
        - 短い方からくっつける
