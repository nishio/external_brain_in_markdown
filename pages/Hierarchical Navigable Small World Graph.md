---
title: "Hierarchical Navigable Small World Graph"
---

[[HNSW]] ([[Hierarchical Navigable Small World Graph]])
[1603.09320 Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs](https://arxiv.org/abs/1603.09320)

[[Skip List]]の高次元版だよねーと思ってたら論文自体にもそう書いてあった

大量のベクトルの中から、与えられたベクトルに近いものを見つけたいというシチュエーションにおいて、素朴に実装するとO(N)になる
- これでは問題があるケースのためにより良い方法が必要
- 従来、1〜3次元くらいでは空間分割をする方法があった(kd-tree)が、今想定しているベクトルは1000次元とかあるので使いにくい
- 近接グラフを使った方法はkd-treeや[[LSH]]に匹敵する性能
- その改善として[[Navigable Small World]] (NSW, also known as Metricized Small World, MSW)が出た
    - = graphs with logarithmic or polylogarithmic scaling of the number of hops during the greedy traversal with the respect of the network size
    - "NSWグラフは、ランダムな順序で要素を連続的に挿入し、先に挿入した要素から最も近いM個の近傍要素に双方向に接続することで構築される。"
    - "構築の最初に挿入された要素の最近傍へのリンクは、後にネットワークハブ間のブリッジとなり、全体的なグラフの接続性を維持し、貪欲なルーティング中にホップ数の対数スケーリングを可能にする。"
    - 何を言ってるのかよくわからないので論文を遡ってみる
    - [[Approximate Nearest Neighbor Search Small World Approach]]
        - 探索の方法としては開始頂点から「もっとも距離が短くなる隣接頂点」へと遷移することを繰り返してローカルミニマムに到達したらそれを返す
            - マルチサーチではランダムな開始点からそれを並列で行う
        - 頂点の追加について
            - ![image](https://gyazo.com/96e01867c473d89d66bda7ec12ea5845/thumb/1000)
            - 2: マルチサーチをする
            - 3: ローカルミニマムからさらに1ステップリンクをたどる
            - 4: ソートして近い方からk本リンクする
            - 要するにランダムに選ばれた各クラスターの中でクエリーにもっとも近い点が選ばれて、その周辺も含めて近い順に繋がれる
                - なので近くに1つのクラスターしかなければそのクラスターだけにリンクが生じる
                - 複数のクラスターをブリッジするような位置にクエリーの点が来ていれば、そのクラスターをつなぐリンクが生成される
- で、これを階層的にしたのが今回の提案
    - > 最大層lが指数関数的に減衰する確率分布でランダムに選択される。
        - これによって、より上位の層に入ることができる頂点が、より長距離のネットワークを形成する
        - 下層にしか入れない頂点たちは近くの頂点とネットワーキングする
    - 探索が階層的になっていて、上位の層で探索した後で、下位の層でその結果をスタートとして探索する
        - 国際線で成田空港に降りてから、鉄道で東京駅に行き、徒歩でサイボウズのオフィスに行く、的なこと
        - ![image](https://gyazo.com/e9a985adac272e88c5b6230e655c77ba/thumb/1000)


応用
- > [[Qdrant]] currently only uses HNSW as a vector index. HNSW (Hierarchical Navigable Small World Graph) is a graph-based indexing algorithm.
- [[Pinecore]]も同じ仕組み [Hierarchical Navigable Small Worlds (HNSW) | Pinecone](https://www.pinecone.io/learn/hnsw/)
- [[ベクトル検索]]のほとんどの実装がこれ

[[階層的]]
[[スモールワールド]]
