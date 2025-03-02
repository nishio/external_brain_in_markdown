
[D - Coloring Edges on Tree](https://atcoder.jp/contests/abc146/tasks/abc146_d)
- ![image](https://gyazo.com/f92ad9c821a31ec19ce1d7da94a425ee/thumb/1000)
- 考えたこと
    - 考察するまでもなく自明な気がするが、言語化しないとだな
    - ツリーだから合流はなく、つまり親から色Xの辺でやってきた頂点はXを除いた色で塗ればいい、それによって矛盾が発生することはない
    - 必要な最小色数は頂点の最大位数
    - 適当な頂点を根として塗っていけば良い
- 公式解説
    - その通り
