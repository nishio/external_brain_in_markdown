---
title: "ScratchExtensionCode"
---

[[Scratch拡張]]のコードをここに書くとScrapboxのAPIでコード単体のURLができるのでそれをsheeptester.github.ioに読みこませて試してる。

ScratchのコードはWebWorkerで走ってるみたいで、JS拡張からwindow.promptを呼び出しても未定義になる
:

```
vm Primitive rejected promise:  ReferenceError: prompt is not defined
   at Prompt._prompt (prompt.js:23)
   at WorkerDispatch.transferCall (extension-worker.js:735)
   at WorkerDispatch.call (extension-worker.js:700)
   at WorkerDispatch._onMessage (extension-worker.js:879)
```

prompt.js

```javascript
class Prompt {
  constructor() { }
  getInfo() {
    return { 
      id: 'prompt',
      name: 'Prompt',
      blocks: [
        {
          opcode: '_prompt',
          blockType: Scratch.BlockType.REPORTER, 
          text: 'prompt([X])', 
          arguments: {
            X: {
              type: Scratch.ArgumentType.STRING, 
              defaultValue: 'message' 
            },
          }
        }
      ]
    }
  }
  _prompt(args) { 
    return prompt(args.X); 
  }
}
Scratch.extensions.register(new Prompt());
```

[https://scrapbox.io/api/code/nishio/ScratchExtensionCode/prompt.js](https://scrapbox.io/api/code/nishio/ScratchExtensionCode/prompt.js)

動いた
from [https://www.kodomonokagaku.com/wp-content/uploads/2020/11/第42回2009ジブン専用パソコン単P-1.pdf](https://www.kodomonokagaku.com/wp-content/uploads/2020/11/第42回2009ジブン専用パソコン単P-1.pdf)
KoKa.js

```javascript
class KoKa {
  constructor() { }
  getInfo() {
    return { 
      id: 'koka',
      name: 'KoKa',
      blocks: [
        {
          opcode: 'power',
          blockType: Scratch.BlockType.REPORTER, 
          text: '[X]の[N]乗', 
          arguments: {
            X: {
              type: Scratch.ArgumentType.NUMBER, 
              defaultValue: '2' 
            },
            N: {
              type: Scratch.ArgumentType.NUMBER,
              defaultValue: '3' 
            }
          }
        }
      ]
    }
  }
  power(args) { 
    return Math.pow(args.X, args.N); 
  }
}
Scratch.extensions.register(new KoKa());
```

[https://scrapbox.io/api/code/nishio/ScratchExtensionCode/KoKa.js](https://scrapbox.io/api/code/nishio/ScratchExtensionCode/KoKa.js)
