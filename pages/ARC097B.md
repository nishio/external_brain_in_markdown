
[D - Equals](https://atcoder.jp/contests/arc097/tasks/arc097_b)
- ![image](https://gyazo.com/12b2768f38990be7bdb5dd3a2aaf087f/thumb/1000)
- 考えたこと
    - 交換は何度でもできるので、交換で繋がった連結成分の中では自由に並べ直すことができる
    - UnionFindで連結成分を求めて、各iについてpiとiが同じ成分であるかチェックして数えれば良い
- 公式解説
    - 証明
