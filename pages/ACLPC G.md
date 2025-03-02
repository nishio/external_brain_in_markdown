
from [[AtCoder Library Practice Contest]]
ACLPC_G
[G - SCC](https://atcoder.jp/contests/practice2/tasks/practice2_g)
- ![image](https://gyazo.com/3f039350389b2300aa35f5bf74deb838/thumb/1000)
- [[強連結成分]]分解をする
    - [Strongly connected component - Wikipedia](https://en.wikipedia.org/wiki/Strongly_connected_component)
    - [強連結成分分解の意味とアルゴリズム | 高校数学の美しい物語](https://mathtrain.jp/kyorenketsu)
    - [ei1333's page](https://ei1333.github.io/algorithm/strongly-connected-components.html) C++
- 深さ優先で探索し戻りがけ順に番号を振る
- 辺を反転し、先の番号の大きい順に再度深さ優先探索をする。たどれた範囲が強連結成分