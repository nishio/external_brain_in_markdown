---
title: "urllib.parse.quote"
---

[[Python3]]
デフォルトでは/がエスケープされない。これはsafeパラメータで制御できる。
python

```
>>> urllib.parse.quote("A/B")
'A/B'
>>> urllib.parse.quote("A/B", safe="")
'A%2FB'
```

