
- `[S. Rendle, 2010]` [PDF](https://www.csie.ntu.edu.tw/~b97053/paper/Rendle2010FM.pdf)
- 二次の組み合わせ特徴量を素朴に扱うと特徴量の数をDとしてD^2のパラメータが生まれてしまう
- そこで各特徴量にK次元のベクトルを割り振り、組み合わせ特徴の重みはそのK次元ベクトルの内積であるという制約を掛ける
- つまりこう $\hat{y}(\mathbf{x}) := w_0 + \sum_{i=1}^n w_i x_i + \sum_{i=1}^n \sum_{j=i+1}^n \langle \mathbf{v_i}, \mathbf{v_j} \rangle x_i x_j$
- これによってパラメータ数はD*Kに減る

