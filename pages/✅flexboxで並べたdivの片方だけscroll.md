---
title: "✅flexboxで並べたdivの片方だけscroll"
---

flexboxで2つのdivを左右に並べた時に、左はテキストエリアでコンテンツによっては縦に長くなるからスクロールしたいのだけど、右はメニューなのでそのスクロールを無視して欲しい→できた
![image](https://gyazo.com/760ddd3af20adee6fd532bc56601c690/thumb/1000)

左にmaxHeight: 100%, overflowY: scrollでできるかと思ったがダメだった
- ![image](https://gyazo.com/96c3a387e2a4efdae1229f30061920a6/thumb/1000)

- なぜ？
- MaterialUIのダイアログが中身のサイズを見て振る舞いを変えてるせい？
    - [React Dialog component - Material-UI](https://material-ui.com/components/dialogs/)
    - サイズの変わらないfullscreen dialogに変えたけど同じ挙動だから関係なさそう
- maxHeight: 300pxなら期待した動きになった
    - けど、この300pxの部分は環境によって異なるからどうしたものかな…

→fullscreen dialogにしたからビューポート基準にしてもいいだろうと考えてmaxHeight: 75vhにした

[[Flexbox]]

コード。スクリーンショットの時点とはここでの本題でない横幅のところは変わってます
- [[最小限の横幅のサイドメニュー]]
ts

```typescript
<div style={{ display: "flex" }}>
  <div
    style={{ flexGrow: 1, maxHeight: "75vh", overflowY: "scroll" }}
  >
    <TextareaAutosize ... />
  </div>
  <div
    style={{
      background: "#eee",
      padding: "2px",
    }}
  >
    Menu
  </div>
</div>
```


[[pRegroup-done]]

作ってから[[position: sticky]]を使うという案を教えてもらった
ts

```typescript
<div style={{ display: "flex" }}>
  <div style={{ flexGrow: 1 }}>...</div>
  <div>
    <div
      style={{
        position: "sticky",
        top: "0px",
        background: "#eee",
        padding: "2px",
      }}
    >
      Menu
    </div>
  </div>
</div>
```

[[スティッキーアイテムに兄弟要素が必要、はデマ]]
