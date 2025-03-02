
二次元空間の長方形の区間にaddをし、点で読み出したい
- 別表現: 長方形の集合と点が与えられる。点を含む長方形の数/コストの和が欲しい [[PAST2N]]

[[二次元の片方を時間軸にする]]
- addとreadを片方の軸でソートし時間軸にする
    - ある時点でRange Addし、別の時点で負のRange Addする
    - ![image](https://gyazo.com/2fd0b0bd0c92f206061c4b4ef25c4fec/thumb/1000)
- RangeAddとReadが同じ座標で重なった時
    - 「角も内側」という仕様なら:
        - 開始のRangeAddはReadより先に処理されなければならない。
        - 終了のRangeAddはReadより後に処理されなければならない
    - 座標を0.5ずらす
        - 開始のRangeAdd: x -= 0.5
        - 終了のRangeAdd: x += 0.5
- xの値が取る範囲が大きい時、[[座標圧縮]]が必要
- [[RangeAddは二つのPointAdd]]で実現できる

[[長方形クエリ]]
