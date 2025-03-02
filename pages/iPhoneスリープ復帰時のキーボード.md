
iPhoneスリープ復帰時のキーボード
iPhoneがスリープから復帰した時、一旦消えたキーボードが再度現れることで直近のコンテンツを隠す
ts

```typescript
let prevInnerHeight: number = 0;
setInterval(() => {
  const currentInnerHeight = window.innerHeight;
  if (currentInnerHeight != prevInnerHeight) {
    prevInnerHeight = currentInnerHeight;
    scrollToBottom()
  }
})
```


[[iOS Safari Keyboard]]

[[謎の余白問題]]

[[pKakidashi-done]]
