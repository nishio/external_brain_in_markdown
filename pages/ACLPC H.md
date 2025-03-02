
![image](https://gyazo.com/8226413287676381d2b6bd90036798ef/thumb/1000)

from [[AtCoder Library Practice Contest]]
ACLPC_H
[H - Two SAT](https://atcoder.jp/contests/practice2/tasks/practice2_h)
- ![image](https://gyazo.com/5e370ce12c72189acac9ebddccbfd576/thumb/1000)
- [[強連結成分分解]]を使うことでTwo-SATが解ける [[2-SAT]]
- Two-SATは二つの項のORをANDで繋いだ形の論理式の解を求める問題
    - でも問題Hの場合、Two-SATにするよりその原理を使ってグラフを直接構築する方がわかりやすいと思う
- Two-SATを強連結成分分解に帰着する原理
    - AならばBって関係は有向グラフの辺だと考えられる
    - このグラフの強連結成分を考えると、どれか一つでもTrueなら全部がTrueになるので、全部Trueか、全部Falseかのどちらかである
    - ![image](https://gyazo.com/8226413287676381d2b6bd90036798ef/thumb/1000)
    - $(A \vee B) = (\neg A \Rightarrow B) \wedge (\neg B \Rightarrow A)$によってORは「ならば」に変換できる
    - なのでグラフを構築して強連結成分分解し、成分ごとに真偽値を割り当てていけば解が得られる
        - Aとnot Aが同じ成分に入ってたら充足不可能、違う成分ならAが先の時にTrueとすれば良い
            - この割当で問題が起きないことをきちんと示せてない。一般のグラフではダメな気がする。
- 具体的な問題Hに戻ると「Xiに旗を置いたなら、距離D未満の位置に旗を置いてはいけない」の「ならば」を辺とするグラフを構築して強連結成分分解すればよい