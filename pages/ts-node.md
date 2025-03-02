---
title: "ts-node"
---

[[TypeScript]]を[[node.js]]で動かす
`$ ts-node src/foo.ts `
:

```
import { Foo } from "./Bar";
       ^

SyntaxError: Unexpected token {
```

`$ node -v`
- v11.14.0

`$ node -v`
- v13.9.0
:

```
(node:39469) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.
import { Foo } from "./Bar";
^^^^^^

SyntaxError: Cannot use import statement outside a module
```


tsconfig.json
diff

```
- "module": "esnext",
+ "module": "commonjs",
```

これで動くようになったのだが、[[umd]]とかの方が良いのだろうか？
