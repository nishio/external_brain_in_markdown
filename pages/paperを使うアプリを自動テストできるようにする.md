
[[paper.js]]を使うアプリを[[自動テスト]]できるようにする

[[paper.js]]はrequireするだけでcanvasを触ろうとするので[[create-react-app]]のデフォルトのテストランナーではテストできない
:

```
Test suite failed to run
Canvas [object HTMLCanvasElement] is unable to provide a 2D context.
> 1 | let paper = require("paper");
```


そこで[[jest-electron]]に変更した

from [[pRegroup-done-2020]]
