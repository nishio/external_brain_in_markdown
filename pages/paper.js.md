---
title: "paper.js"
---

ts

```typescript
const paper = require("paper");

function App() {
  useEffect(() => {
    var canvas = document.getElementById("myCanvas");
    paper.setup(canvas);
    var path = new paper.Path();
    path.strokeColor = "black";
    var start = new paper.Point(100, 100);
    path.moveTo(start);
    path.lineTo(start.add([200, -50]));
    paper.view.draw();
  }, []);
  return (
    <div className="App">
      <div>
        <canvas
          id="myCanvas"
          data-paper-resize="true"
          style={{ height: "100vh", width: "100vw" }}
        ></canvas>
      </div>
    </div>
  );
}
```



---
[http://paperjs.org/](http://paperjs.org/)

> Paper.js is based on and largely compatible with [[Scriptographer]]
- [[Adobe Illustrator]]

- apple pencilで字を書いて支障ないレスポンス速度だった
- [http://paperjs.org/examples/path-simplification/](http://paperjs.org/examples/path-simplification/)

- `$ npm install paper`
- `var paper = require("paper");`

[http://paperjs.org/tutorials/paths/smoothing-simplifying-flattening/](http://paperjs.org/tutorials/paths/smoothing-simplifying-flattening/)
