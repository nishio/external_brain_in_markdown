---
title: "AtCoderのPythonでMemoryErrorを出すとREになる"
---

python

```
xs = [0] * (10 ** 9)
```

![image](https://gyazo.com/7a3c6eaea86deec2d0977e4c21e18fa7/thumb/1000)

こういうケースは、実際にメモリを確保してメモリ制限を超えるより前に、Python処理系が「そんな量の確保はできないよ」と実行時例外を投げている。なのでジャッジサーバ上の表示はMLEではなくREになる。
