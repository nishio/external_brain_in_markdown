---
title: "REGROUP-10"
---

`REGROUP-10 - TypeError: undefined is not an object (evaluating 'o[t[0]].parent')`
iPad上で投げ縄選択して移動した後、選択したかったものと違うものが移動される
- 選択のタイミングでそもそも座標がずれている？
:

```
TypeError: undefined is not an object (evaluating 'o[t[0]].parent')
  at moveItems (moveItems.ts:49:21)
  at onDragEnd (Lasso.ts:171:7)
  at onDragEnd (mouseEventStateManager.ts:413:19)
  at apply (mouseEventStateManager.ts:111:5)
```


再現方法不明

[[pRegroup]]
