
- [[最大流]]を求めるアルゴリズム
    - DinicはO(V^2E)
- [[最大流を求めるアルゴリズムの歴史]]
- [AOJ GRL_6_A 最大流](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=GRL_6_A&lang=jp)で実装の検証ができる
- 僕のPython実装(AOJで検証済み)
    - 辺はdefaultdict(dict)で待ってるので逆辺の取得のために逆辺のindexを持つ必要はない
        - (多くのC++実装では各辺に逆辺のindexを持たせてる)
    - 「探索済み辺を探索しない」
        - これを「まだ探索してない辺の最初のindex」を`itertion_count`に持つことで実現している
        - これを使うためにはindexから辺への対応づけが必要だから`max_flow`の中で最初に作ってる: `edges_index`
- [GitHub](https://github.com/nishio/atcoder/blob/master/libs/dinic_maxflow.py)


他の人の実装
- [[蟻本]]　p.194
- [http://algoogle.hadrori.jp/algorithm/dinic.html](http://algoogle.hadrori.jp/algorithm/dinic.html)
- [https://ei1333.github.io/luzhiled/snippets/graph/dinic.html](https://ei1333.github.io/luzhiled/snippets/graph/dinic.html)
- [https://tubo28.me/compprog/algorithm/dinic/](https://tubo28.me/compprog/algorithm/dinic/)
- [http://www.prefield.com/algorithm/graph/dinic.html](http://www.prefield.com/algorithm/graph/dinic.html)


[[最大二部マッチング]]
