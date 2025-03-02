
[C - One-stroke Path](https://atcoder.jp/contests/abc054/tasks/abc054_c)
![image](https://gyazo.com/d709f17d39572be0e97aa653b895f2fe/thumb/1000)
![image](https://gyazo.com/dfc5b8b3a15d7b70e7ca6c8340950de9/thumb/1000)

- 考えたこと
    - [[計算量の見積もり]]
        - 頂点数が8だから階乗で全探索してもOKだな
    - 普段グラフは隣接リストで持つんだけど、今回は隣接行列だな
    - 各順列について「辺があるか」をチェックすればOK
    - 途中で辺がなければ先を探索しても無理なので深さ優先探索で枝刈りするのがいいね
- 公式解説OK
    - 上記で想定解法だがbit DPでO(N^2 2^N)になるそうだ
        - 部分集合すべてについて点Xから開始して全部をたどって点Yで終わる場合の数をもつのだな
