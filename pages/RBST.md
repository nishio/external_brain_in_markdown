
Randomized Binary Search Tree
- [[ABC170 E]]の解説で
    - > 順序付き多重集合は C++ の multiset などを用いることで高速に処理することができます。
    - と書かれていたため、C++のmultisetに相当するものはPythonだと何？と話題になった
        - [[Pythonでmultiset]] heapqを使ってなんとかするケースが多い
        - Pythonの標準ライブラリには[[平衡二分木]]がない
            - 自前ライブラリとして持っておくといいのでは…という気持ちになった

- ノードをオブジェクトとして作ってるような実装は全般的に筋悪
    - オブジェクトの生成コストが高いので。
    - 配列で実装してnumbaでコンパイルする方針で作る

- ABC170Eで [AC](https://atcoder.jp/contests/abc170/submissions/14654208) した


--- 開発
- C++実装をPythonに移植した
    - [k 番目の値を高速に取り出せるデータ構造のまとめ - BIT上二分探索や平衡二分探索木など - Qiita](https://qiita.com/drken/items/1b7e6e459c24a83bb7fd)で紹介されてるのを素朴に移植
    - [https://github.com/nishio/atcoder/blob/master/memo/rbst_normal.py](https://github.com/nishio/atcoder/blob/master/memo/rbst_normal.py)
- [[ABC170 E]]の[[フェニック木]]での実装をRBSTに置き換えて全テストコードでACすることを確認
    - フェニック木での実装　4.83sec
    - RBSTでの実装　105.47sec
    - 20倍遅い
- クラスを取り除く
    - 67.01sec
    - 6割ほど速くなった
- 再起呼び出しを取り除き[[numba]]でコンパイル
    - 10.13sec
- リストでの逐次追加をnp.arrayでの一括アロケーションに変えた
    - 4.60sec
