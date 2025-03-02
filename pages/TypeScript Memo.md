---
title: "TypeScript Memo"
---

ts

```typescript
let state: ({ type: "INITIAL", value: null } | { type: "WITH_NUMBER", value: number })
const f = () => {
  if (state.type === "WITH_NUMBER") {
    let x: number = state.value;
  }
}
const f2 = () => {
  const type = state.type;
  if (type === "WITH_NUMBER") {
    // let x: number = state.value;  // NG
    // Type 'number | null' is not assignable to type 'number'.
  }
}
```


ts

```typescript
// before
if (dragStartType === "RootPiece") {
  if (target !== null && isPiecePaperItem(target)) {
    updatePiecePosition(target);
    deselect(target);
  } else {
    throw new Error("never");
  }
}
//after
if (mouseState.type === "RootPiece") {
  updatePiecePosition(mouseState.target);
  deselect(mouseState.target);
}
```

