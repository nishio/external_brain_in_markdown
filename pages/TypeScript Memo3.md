
ts

```typescript
  deselect(mouseState.target);
  if (handler !== null) {
    handler.onClick(event);
    handler = null;
    return;
  }
  
  ...
  
  const deselect = (x: PaperItem | null) => {
    if (x != null) {
      ...
    }
  }
```


ts

```typescript
  if (
    mouseState.type === "Nothing" ||
    mouseState.type === "Nothing_WithShift"
  ) {
    mouseState.handler.onClick(event);
    mouseState = INITIAL_STATE;
    return;
  }
  deselect(mouseState.target);

...

const deselect = (x: PaperItem) => {
  ...
}
```


