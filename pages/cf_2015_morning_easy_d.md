---
title: "cf_2015_morning_easy_d"
---

[https://atcoder.jp/contests/code-festival-2015-morning-middle/tasks/cf_2015_morning_easy_d](https://atcoder.jp/contests/code-festival-2015-morning-middle/tasks/cf_2015_morning_easy_d)
- 考えたこと
    - 文字列を二回の部分文字列の繰り返しにしたい問題
    - 二回目の開始点がどこかわからない
    - 食い違った時にどちらを読み飛ばすかで2通りあるよな
    - うーむ
    - 理論上は二回目の開始点が2文字目からにもなり得るが、その時には最良でもコストがN-2なのだな
    - 二回目の開始点n, 注目点i, jの三つ組を考える
    - (n, 0, n)からスタートして(n, n, N)にたどり着けばゴール
    - Si=Sjならゼロコストでi,jをインクリメントできる
        - 違うならコスト1で片方をインクリメントできる
    - つまりこれは[[最短経路問題]]で、[[ダイクストラ法]]で解けば良い。グラフは明に構築はしない
    - Nが100なので頂点数は5×10^5程度。余裕。
- 公式解説なし
