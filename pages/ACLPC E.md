
![image](https://gyazo.com/eaaba4778f81bf4f4751b1e923ffae74/thumb/1000)



from [[AtCoder Library Practice Contest]]
ACLPC_E
[E - MinCostFlow](https://atcoder.jp/contests/practice2/tasks/practice2_e)
- ![image](https://gyazo.com/4a918321865b3d3cb12a58f05b197d54/thumb/1000)
- [[最小費用流]]
    - [最小費用流(Primal-Dual) | Luzhiled’s memo](https://ei1333.github.io/luzhiled/snippets/graph/primal-dual.html)
- 「選ばれるものがK個以下」はフローの言葉にすると「容量Kの辺が繋がってる」ということ
- 選ばれるマスは容量1の辺にしておいて、最小費用流を求めた時にフローがある辺が「選ばれたマス」になる
- 選ぶとXの得をする選択肢は、選ばないとき大きな値INFの費用が掛かるようにしておいて、選ぶとINF-Xの費用がかかるようにすれば良い
    - ![image](https://gyazo.com/5a9d6fb8d110d875509cebc706ad10e7/thumb/1000)![image](https://gyazo.com/025a8b01a2bac694b9a720de4339d0d1/thumb/1000)
    - ![image](https://gyazo.com/eaaba4778f81bf4f4751b1e923ffae74/thumb/1000)

