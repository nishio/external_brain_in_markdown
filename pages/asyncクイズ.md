---
title: "asyncクイズ"
---

[https://twitter.com/tkihira/status/1429061261895946240?s=21](https://twitter.com/tkihira/status/1429061261895946240?s=21)
js

```javascript
// どういう順番で表示されるでしょうか？
console.log(1);
(async () => {
  console.log(2);
  await new Promise(r => {
    setTimeout(r, 1000);
    console.log(3);
  });
  console.log(4);
})();
console.log(5);
```


>  An async function expression can be used as an IIFE (Immediately Invoked Function Expression) which runs as soon as it is defined.
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/async_function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/async_function)

> The body of an async function can be thought of as being split by zero or more await expressions. Top-level code, up to and including the first await expression (if there is one), is run synchronously. In this way, an async function without an await expression will run synchronously. If there is an await expression inside the function body, however, the async function will always complete asynchronously.
[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

