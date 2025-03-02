
> data-paper-resize="true"

ts

```typescript
window.app.paper.project.view.onResize = () => {
  window.app.paper.project.view.center = center;
}
```


まだやってないけど、[[画面移動の際に直前のcenterを保存]]しておくようにする。
そうすると上記のようにキャンバスサイズが変わった時に中心を保つことができる

[[Paper.js]]
