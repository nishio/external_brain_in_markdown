
Paper.jsの再描画は非同期に行われているっぽい
それ自体はよいこと？なのだが

- PaperのZoomの値を設定
- Imageを消す
- Paperを表示

って処理をすると

- Imageが消える
- ズーム前のPaperが表示される
- その後ズームされたPaperが表示される

ってなって見栄えが最悪。
Paperに再描画終了後に呼ばれるハンドラとかあるかな、Imageを消すのを遅らせたい。

setZoomはMatrixの変更を引き起こしてる
[https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/basic/Matrix.js#L382](https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/basic/Matrix.js#L382)
それが_changedを呼ぶ

これが画面全体を削除して再描画している
[https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/CanvasView.js#L132](https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/CanvasView.js#L132)
これがおそらく非同期に呼ばれるのだと思うがどこで呼ばれているのか

ここでDomEvent.[[requestAnimationFrame]]している
[https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/View.js#L222](https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/View.js#L222)

なので今僕が求めている「描画完了時にコールバックしてほしい」って点に関しては
[https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/CanvasView.js#L142](https://github.com/paperjs/paper.js/blob/cc135eaba80943f78075f84ca430dc3152bd154e/src/view/CanvasView.js#L142)
ここにコールバックの呼び出しがあってほしいわけだが、現状ない。
→モンキーパッチを当てる

ts

```typescript
  window.app.paper.project.view.__proto__.update = function() {
      if (!this._needsUpdate)
          return false;
      var project = this._project,
          ctx = this._context,
          size = this._viewSize;
      ctx.clearRect(0, 0, size.width + 1, size.height + 1);
      if (project)
          project.draw(ctx, this._matrix, this._pixelRatio);
      this._needsUpdate = false;
      if(window.app.callbackAfterCanvasViewUpdate){
        window.app.callbackAfterCanvasViewUpdate();
      }
      return true;
  }
```

とやっておいて
ts

```typescript
  window.app.callbackAfterCanvasViewUpdate = () => {
      image.style.display = "none";
      let canvas = document.getElementById("myCanvas") as HTMLElement;
      canvas.style.display = "inline";
      window.app.callbackAfterCanvasViewUpdate = null;
  }
```

って感じ。

[[pRegroup-done-2019]]
