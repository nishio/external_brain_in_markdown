
[[VSCode]]の[[autopep8]]が原因でsys.pathの設定より前にimportが移動されてimportできなくなる問題
`nopep8`すれば良い
python

```
sys.path.append("../bert")
import modeling  # nopep8
```


