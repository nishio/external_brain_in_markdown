---
title: "indeednow_2015_qualc_C"
---

[C - 木](https://atcoder.jp/contests/indeednow-qualb/tasks/indeednow_2015_qualc_3)
- ![image](https://gyazo.com/2908a294054ddde75f3d5615245d2b40/thumb/1000)
- 考えたこと
    - 素朴にやると「隣接してる頂点の中から最も小さいものを取る」を繰り返せばよい
    - しかしこの方法だと頂点1から他の10^5個に辺があったときに10^5個からの選択を10^5回くらいするので間に合わない
    - というわけで毎回検索したりソートしたりしないで最小の値が取れる方法が必要
    - [[優先度キュー]]だね
- [[公式解説OK]]
