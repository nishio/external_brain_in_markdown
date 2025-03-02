---
title: "Macbookのトラックパッドで拡大縮小平行移動"
---

ブラウザ上の対象をトラックパッドの二本指ジェスチャーで上下左右に動かしたり拡大縮小をしたい

結論
- これらの操作はwheelイベントでブラウザに伝えられる
- deltaX, deltaYに縦横の移動量が入っている
- ピンチの場合はctrlKey: trueになっている
- wheelイベントはデフォルトでpassiveなのでブラウザのデフォルトのスクローン操作を止めるためにはまずpassiveをオフにする必要がある
    - `window.addEventListener("wheel", onWheel, { passive: false });`
    - see [EventTarget.addEventListener() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)




---memo
from [[pMovidea]]
Macbookのタッチパネルで平行移動
- [Detecting multi-touch trackpad gestures in JavaScript](https://kenneth.io/post/detecting-multi-touch-trackpad-gestures-in-javascript)
- ホイールイベントにXとYがある
    - (Zもある)
- ピンチの場合はctrlKey: true
    - マジかよ(マジだった)
