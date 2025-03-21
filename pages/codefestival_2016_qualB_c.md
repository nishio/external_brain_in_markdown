---
title: "codefestival_2016_qualB_c"
---

[https://atcoder.jp/contests/code-festival-2016-qualb/tasks/codefestival_2016_qualB_c](https://atcoder.jp/contests/code-festival-2016-qualb/tasks/codefestival_2016_qualB_c)

- 考えたこと
    - 点が長方形に並んでて[[最小全域木]]を作る問題
    - 点が10^10あるので陽に全域木を作るわけではなさそう
    - [[端から埋める]]
        - 角の家は2通りの繋がり方しかないので小さい方で繋がれば良い
        - これを縦であると考えても一般性を失わない
        - 接続先もまた2通りの繋がり方しかない
            - これが下の場合、再起的に同じ議論が繰り返される
        - もし横である場合、その道は上に動かしてもコストが変わらない
        - うーん
    - [[クラスカル法]]を考える
        - 最短の頂点を選んでそれをつなげる
        - 今回の問題条件ではiとi+1を繋ぐ道が全部同じコスト
        - 縦横のコストの中で最小のものを一つ選ぶ
            - それを全部縮約すると、少し小さい長方形になる
                - ![image](https://gyazo.com/2916eb83214b0fd8a81a9816918f646a/thumb/1000)
            - 点になるまで繰り返せば OK
            - それはつまり全部使うということ
            - p,qをそれぞれソートして$\sum_i p_i (H-i)$
- 公式解説
    - 最後の一歩でWAした、縦を繋いだ時に、横の本数が減るので、まとめてソートして順に計算するべきだった
    - [[グリッドグラフ]]
