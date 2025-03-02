---
title: "スライドRange Argminを優先度キューで"
---

![image](https://gyazo.com/daf92a2b122d491eedaa4ea8299587a2/thumb/1000)
範囲が一方向にスライドしていく[[Range min]]/[[Range argmin]]は[[優先度キュー]]で実現できる
- 優先度キューに(値, 場所)を入れる
- 範囲に新しく入るものをキューに追加する
- 最小値を読み出した際に、範囲外なら読み飛ばせば良い

[[PAST2L]]
