---
title: "open with quartz"
---

![image](https://gyazo.com/d6d06600842235c8f1618ce891f8690a/thumb/1000)


script.js

```javascript
const onClick = () => {
  location.href = location.href.replace('scrapbox.io/nishio','nishio.github.io/quartz');
};

scrapbox.PageMenu.addMenu({
  title: "quartz",
  image: "https://gyazo.com/d6d06600842235c8f1618ce891f8690a/raw",
  onClick,
});
```

