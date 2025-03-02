---
title: "CSSで条件分岐と変数と計算を使う"
---

- [[メディアクエリ]]で条件分岐ができる
    - [メディアクエリの使用 - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/Media_Queries/Using_media_queries)
    - 印刷画面と通常画面を切り替えるものってイメージでいた(メディアっていうし)
    - しかし画面サイズを条件式に加えることができる
- [[カスタムプロパティ]]で変数を作れる
    - [CSS カスタムプロパティ (変数) の使用 - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/Using_CSS_custom_properties)
    - :root 擬似クラスがグローバルスコープがわりに使える
- calc()で計算できる
    - [calc() - CSS: カスケーディングスタイルシート | MDN](https://developer.mozilla.org/ja/docs/Web/CSS/calc)
- JSで取得できる
    - `getComputedStyle(document.body).getPropertyValue("--toolbar-height")`
    - stringなので単位を仮定したらこんな感じ
ts

```typescript
const toolbarHeight = parseInt(
    getComputedStyle(document.body)
      .getPropertyValue("--toolbar-height")
      .trim()
  );
```


横幅が狭い時にツールバーの高さを縮めてボタンも小さくするcss
css

```
:root {
  --toolbar-height: 60px;
}
@media only screen and (max-width: 600px) {
  :root {
    --toolbar-height: 36px;
  }
}

#toolbar {
  height: var(--toolbar-height);
}
#toolbar svg {
  height: calc(var(--toolbar-height) * 0.8);
  margin: calc(var(--toolbar-height) * 0.1) 0 calc(var(--toolbar-height) * 0.1) 0;
}
```

最近の[[CSS]]は便利！

css

```
/* ボタン7つを３グループに分けるスペーサー */
#toolbar span.spacer {
  margin-left: calc((100vw - var(--button-size) * 7) / 2);
}
```


余談
- クラス名にパターンマッチもできる
    - [Attribute selectors - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors?fbclid=IwAR0QOFAM0qUYu8eWeDTveDUrH3fbEhYRh3ocF-6M-z61wrfdELQitgcOdfs)
