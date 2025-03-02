---
title: "選択範囲のHTML取得"
---

js

```javascript
x = window.getSelection().getRangeAt(0).cloneContents()
div = document.createElement('div')
div.appendChild(x)
div.innerHTML
```

ドキュメントフラグメントはinnerHTMLを取得できないが、divに入れてしまえば取得できる

[[pLinkSuggest]]
