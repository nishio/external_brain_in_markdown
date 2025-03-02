---
title: "Tool選択を改善"
---

from [[pRegroup2020]]
Tool選択を改善
    - 「Paper.jsのTool#activateを読んでからsetState」ってやっていて、setStateを忘れたバグなんだけど
    - そもそも「setState→useEffectでTool#activateが呼ばれる」が正しい。
    - どこに書いてあったか忘れたけど"[[single source of truth]]"って考え方。
    - Reactがsingle sourceになり、そこを編集した時にPaper.js側が従属して更新されるようにすべきだった。
