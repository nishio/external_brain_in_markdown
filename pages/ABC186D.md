---
title: "ABC186D"
---

from [[ABC186]]
ABC186D
![image](https://gyazo.com/ea141db402b5efb6d1a5ec855b4fcfab/thumb/1000)
- ![image](https://gyazo.com/9ab4d650ada0faeb834057b1ca1f25ea/thumb/1000)
- [D - Sum of difference](https://atcoder.jp/contests/abc186/tasks/abc186_d)
- Twitter上では累積和を使うという話が多いですが僕は累積和を使ってません。
- ソートして隣接した項の差をとったものをDiとするなら解の中のDiの出現回数はi(N-i)なので掛けて足すだけ。
    - ![image](https://gyazo.com/ea141db402b5efb6d1a5ec855b4fcfab/thumb/1000)
    - $S = \sum_{i=1}^{N-1} D_i i (N - i) = \sum_{i=0}^{N-2} D_i (i+1)(N-i-1)$
python

```
def main():
    N = int(input())
    AS = list(map(int, input().split()))
    AS.sort()
    DS = []
    for i in range(N - 1):
        DS.append(AS[i + 1] - AS[i])
    ret = 0
    for i in range(N - 1):
        ret += DS[i] * (N - 1 - i) * (i + 1)
    print(ret)
```

- ところでTwitterを見てたら「なんでソートしていいの？」という投稿があった
    - 求める値はN個の値から2つを取り出すすべての組み合わせに対して、2つの数の順序によらない数を足し合わせてる
    - ![image](https://gyazo.com/f2f8d759d6ee863c0e635f31664dabe5/thumb/1000)

    - 対称性から順序をどのように入れ替えても結果が変わらない
    - だから扱いやすい「ソートされてるもの」にした
- [[ソートをして絶対値を外す]]
- [[足し算の順序の変更]]
- [[対称なので並び替えて良い]]
    - [[順序は関係ない]]
