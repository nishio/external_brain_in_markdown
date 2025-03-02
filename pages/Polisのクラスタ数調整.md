---
title: "Polisのクラスタ数調整"
---

PolisのClojureで実装されたmathサーバの中に書かれている

math/src/polismath/math/conversation.clj:509
clj

```
(range 2 (inc (max-k-fn group-cluster-proj (:max-k opts')))))]))
```

:142
clj

```
(merge {:n-comps 2 ; does our code even generalize to others?
        :pca-iters 100
        :base-iters 100
        :base-k 100
        :max-k 5
        :group-iters 100
        ;; These three in particular we should be able to tune quickly
        :max-ptpts 100000
        :max-cmts 10000
        :group-k-buffer 4}
  opts))
```


この`(range 2`と`:max-k 5`をそれぞれ4にしたら確定で4個のクラスターができるのではないか
