---
title: "useCallback"
---

[[React Hooks]] [Hooks API Reference – React](https://reactjs.org/docs/hooks-reference.html#usecallback)

js

```javascript
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```


- `useCallback(fn, deps)`は「depsが変化した場合のみfnを呼び出す関数」を作る
- fnに引数が渡されるわけではない。外のスコープから読む。
- 注目したい値(deps)以外の変更ではfnが呼び出されないように刈り込みたい時に使う
- useCallback(fn, deps) は useMemo(() => fn, deps) と等価 [[useMemo]]
- fnの中で使う値はdepsの中で列挙されているべきである(設計思想)
    - コンパイラが進歩したらdepsは自動生成される
    - exhaustive-deps ルールによってESLintでチェックできる