---
title: "DaisyDisk"
---

[DaisyDisk | Home](https://daisydiskapp.com/)

[【Mac Info】Macのストレージがいっぱい!?　定番の「DaisyDisk」で整理しよう - PC Watch](https://pc.watch.impress.co.jp/docs/column/macinfo/1469474.html)

[[Docker]]が巨大だった
:

```
% docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          20        2         70.51GB   64.21GB (91%)
Containers      2         0         23.88MB   23.88MB (100%)
Local Volumes   0         0         0B        0B
Build Cache     191       0         20.38GB   20.38GB
```


`$  docker container prune`
`$  docker image prune`
`$  docker builder prune`

:

```
% docker system df      
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          14        0         57.57GB   57.57GB (100%)
Containers      0         0         0B        0B
Local Volumes   0         0         0B        0B
Build Cache     92        0         0B        0B
```

