
from [[競技プログラミングで解法を思いつくための典型的な考え方]]
JOI2008HO_C
[PDF](https://www.ioi-jp.org/joi/2007/2008-ho-prob_and_sol/2008-ho.pdf#page=6)
![image](https://gyazo.com/503913df0873f6aed45912d413fa40a1/thumb/1000)
- [https://atcoder.jp/contests/joi2008ho/tasks/joi2008ho_c](https://atcoder.jp/contests/joi2008ho/tasks/joi2008ho_c)
- 1000個の値から4つ以下選んで足したもののうちMを超えない最大値を求める
- 0〜2個の組み合わせでできる数を事前に列挙して、ソート、足してもMを超えない最大の数を二分探索で求める
- [[半分全列挙]]
- #TODO 間違ってそう
