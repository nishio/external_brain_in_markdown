
Pythonに[[multiset]]が欲しいという意見がよくある e.g. [[ABC170 E]]
だいたいのことが[[heapq]]との組み合わせでできる

- [[heapq]]
    - O(logn)で要素の挿入
    - O(1)で最小値の取得
- [[heapq]]とdict(ハッシュテーブル)の組み合わせ [[heapq+dict]]
    - [Pythonでmultisetの代用ができるデータ構造 - Tsuboの競プロブログ](https://tsubo.hatenablog.jp/entry/2020/06/15/124657)
    - O(logN)で要素の挿入、削除
    - O(1)で要素の存在確認、最小値の取得
    - 二分探索ができない
- 二分探索
    - 事前にソートして良いなら[[bisect]]
        - k番目の値は読むだけ。O(1)
        - 「kを超える最初の場所」がright、「k以上の最初の場所」がleft
    - 固定のk番目の値が欲しい→ [[heapq]]
        - [k 番目の値を高速に取り出せるデータ構造のまとめ - BIT上二分探索や平衡二分探索木など - Qiita](https://qiita.com/drken/items/1b7e6e459c24a83bb7fd)
    - [[フェニック木]] [[BIT]]
        - 値域のサイズD
        - 二分探索 O(logD)
        - 追加削除はO(logD)
        - [[座標圧縮]]でDを圧縮することが効果的
        - 「k番目の値」も「kを超える最初の値」も両方できる
- [[平衡二分木]]
    - [[RBST]]
    - AVL木
        - [https://juppy.hatenablog.com/entry/2019/02/26/python_AVL木_配列ver_競技プログラミング_Atcoder_](https://juppy.hatenablog.com/entry/2019/02/26/python_AVL木_配列ver_競技プログラミング_Atcoder_)

- 「順序付き集合は平方分割が速い」らしい(未確認
    - [https://nagiss.hateblo.jp/entry/2019/06/04/220541](https://nagiss.hateblo.jp/entry/2019/06/04/220541)
        - [https://atcoder.jp/contests/abc140/submissions/7482671](https://atcoder.jp/contests/abc140/submissions/7482671)
- SkipList
    - [https://atcoder.jp/contests/arc033/submissions/14718760](https://atcoder.jp/contests/arc033/submissions/14718760)


- [C - データ構造](https://atcoder.jp/contests/arc033/tasks/arc033_3)


[[データ構造]]
