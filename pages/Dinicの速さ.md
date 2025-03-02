
[[Dinic]]の計算量はO(V^2E)で、EがVに比例する時V=10000では解けなさそうに思うわけだが「現実にはもっと速い」とされて、実際速い、じゃあどれくらい速いのか

- [Dinic 法とその時間計算量 - みさわめも](https://misawa.github.io/others/flow/dinic_time_complexity.html)
    - 辺の容量が整数である時にいくつかの条件で計算量が減る
        - 最大流がFの時 $O(FE)$
        - 辺の容量が高々Cの時$O(C E^{3/2})$
            - かつ多重辺がない時 $O(CV^{2/3}E)$
        - 各頂点を流れるフローが高々Fのとき $O(FV^{1/2}E)$
            - 二部マッチングを最大フローで解く場合は上記のF=1の場合に相当する
    - 動的木を使う実装の場合、一般のグラフに対して $O(VE\log V)$
    - [最大流問題について. - れんしゅうちょう。 - TopCoder部](https://topcoder-g-hatena-ne-jp.jag-icpc.org/Mi_Sawa/20140311/)
    - [最大流問題について その3 - れんしゅうちょう。 - TopCoder部](https://topcoder-g-hatena-ne-jp.jag-icpc.org/Mi_Sawa/20140320.html)

- 辺容量が定数の場合$ O(\min \{ E^{1/2}, V^{2/3} \} E)$ [PDF](https://www.cs.bgu.ac.il/~dinitz/Papers/Dinitz_alg.pdf)

