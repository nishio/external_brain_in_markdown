
from [[F値]]
F値はなぜ調和平均なのか

F値とは [http://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html](http://scikit-learn.org/stable/modules/generated/sklearn.metrics.f1_score.html)
- `F1 = 2 * (precision * recall) / (precision + recall)`
- 最大1最小0
- precision == recall の時にはF値も同じ値
- precision と recall のどちらかが0の時にはF1も0になる
![image](https://gyazo.com/5645c89ab5b98065c1903cee82c3c507/thumb/1000)

- TP: True Positive
- FP: False Positive
- FN: False Negative
- TN: True Negative
- Precision:
- $P = \frac{TP}{TP+FP}$
- Recall:
- $R=\frac{TP}{TP+FN}$
- 逆数の和
- $\frac{1}{P} + \frac{1}{R} = \frac{2TP+FP+FN}{TP}$
- F1 scoreはPとRの調和平均
- $F1 = \frac{2 P R}{P + R} = \frac{2 \frac{TP}{TP + FP} \frac{TP}{TP + FN} }{\frac{TP}{TP + FP} +\frac{TP}{TP + FN}} = \frac{2 TP}{(TP + FN) + (TP + FP)} = \frac{2 TP}{2TP + FN+ FP}$
- $\frac{2}{\frac{1}{P} + \frac{1}{R}} = \frac{2TP}{2TP + FP + FN}$
- Normalized Symmetric Difference [http://www.dcs.gla.ac.uk/Keith/pdf/Chapter7.pdf](http://www.dcs.gla.ac.uk/Keith/pdf/Chapter7.pdf) p.128
- $E = \frac{FP + FN}{2TP + FP + FN}$
- F1とEを足すと1: F1 + E = 1

- Fβスコア
- $F_\beta = \frac{(1 + \beta ^ 2) TP}{(1 + \beta^2) TP + \beta^2 FN + FP}$
- $\frac{1}{P} + \frac{\beta^2}{R} = \frac{(TP+FP)+\beta^2(TP+FN)}{TP}$
- 要するにRecallに$\beta^2$の重みを付けた調和平均
- なぜ$\beta$ではなく$\beta^2$なのか？？
- $F_\beta = \frac{(1 + \beta ^ 2) TP}{(1 + \beta^2) TP + \beta^2 FN + FP} = \frac{1+\beta^2}{\frac{1}{P} + \frac{\beta^2}{R}}$
- 係数は省略してZと書くと
- $\frac{\partial F_\beta}{\partial R} = Z \frac{\beta^2}{R^2}, \frac{\partial F_\beta}{\partial P} = Z \frac{1}{P^2}$
- つまり$\beta P = R$ の時勾配が一致する
- 勾配が一致するということは「PやRを同じだけ動かした時のスコアに対する影響が同じ」ということ。
- RがPよりβ倍大きいときに均衡するということ？