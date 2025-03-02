---
title: "paper.jsでの拡大縮小テスト"
---

from [[pRegroup-done-2019]]
paper.jsでの拡大縮小テスト
- [[付箋の追加をPaper.js上で実装する]]
- [[100枚付箋のiPad上での拡大縮小]]
の前にまずpaper.jsで拡大縮小を試してみて振る舞いを観察すべきだ

- [[Hosting]]なしで試せるかな？
    - ローカルのWifiでiPadから開発サーバを見れるかな、それも試す
    - →同一Wifiに繋げば問題なくiPadからアクセスできる


Paper.jsでのズーム
- `paper.setup(canvas);`
- の後
- `paper.install(window.app.paper);`
- すると
- `window.app.paper.project.view.zoom = 1.3`
- でズームを変えられる(とりあえず)
- setZoomがあるからそれを適当なところにバインドしておくのが良さそう

マルチタッチの扱い
- 素直にこれを写経: [Multi-touch interaction - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Touch_events/Multi-touch_interaction)
- 問題点→[[二本指ジェスチャ時に一本指での描画が同時に発生する問題]]
-----


- [retyui/react-quick-pinch-zoom: A react component that providing multi-touch gestures for zooming and dragging on any DOM element.](https://github.com/retyui/react-quick-pinch-zoom)
- [React Pinch + Zoom + Pan](https://gist.github.com/iammerrick/c4bbac856222d65d3a11dad1c42bdcca)

[[iOS上のChromeでデバッグ出力]]
