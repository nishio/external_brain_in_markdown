---
title: "(解決)Cannot find type definition file for ~"
---

![image](https://gyazo.com/dfa7da2134b74fe47ed0b6fe0154b640/thumb/1000)
- `@types/...`をyarn addしてもダメだった
- `tsconfig.json`に`"types": ["node"]`をつけた

[commit](https://github.com/nishio/kozaneba/commit/1c3eab89e9e7bdd0a00824f623e618da13a3528f)

ref
- [https://stackoverflow.com/questions/54232428/cannot-find-type-definition-file-for-node-in-typescript-react-app](https://stackoverflow.com/questions/54232428/cannot-find-type-definition-file-for-node-in-typescript-react-app)
