
[https://atcoder.jp/contests/code-festival-2014-morning-easy/tasks/code_festival_morning_easy_c](https://atcoder.jp/contests/code-festival-2014-morning-easy/tasks/code_festival_morning_easy_c)

- 考えたこと
    - sからtへの最短経路であって、途中の頂点でちょうど距離の半分になるようなものが存在するかどうかという問題
    - 最短経路は指数的オーダーで存在するので列挙してから調べることはできない
    - まずs,tの距離を求めてからその半分の頂点があるか調べよう
    - ダイクストラ法でs,tの距離を求めた時、それより短い頂点への距離は特定済み
        - そこからちょうど半分の距離のものを選ぶ
            - これは最悪N個近く存在する
        - t,sの距離も同様に求める、かと
        - d(s,v)=d(t,v)=d(s,t)/2であるようなvがあるかを調べれば良い
            - これは線形オーダー
        - 計算量は[[ダイクストラ法]]のものなので間に合う
- 公式解説
    - なし
