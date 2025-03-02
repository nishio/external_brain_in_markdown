---
title: "iPadはfocusを無視することがある"
---

from [[pRegroup-done-2019]]
iPadはfocusを無視することがある
- BUG: 付箋の追加時、PC版ではテキストエリアにフォーカスが当たるのだが、iPadだとなぜか当たらない
    - useEffectのなかでtextarea.focus()してるのだが
- [iOSのMobile Safari上でのfocus()が妙な件を調べてみた - mixi engineer blog](https://alpha.mixi.co.jp/entry/2012/10807/)
- [iPhoneのSafariで入力フィールドにフォーカスが移らない | GWT Center](https://www.gwtcenter.com/iphone-safari-doesnt-get-focus)
- ええー、イベントハンドラの中から直接呼んだ場合を除いてfocusが聞かないってことは、そもそもイベントハンドラで状態を更新してReactがその状態更新を見てdisplay:noneを解除しているような今回のケースではどうしようもないってことじゃないか
- ボタンのTouchstartでReactに任せずに直接display & focus
- →done
