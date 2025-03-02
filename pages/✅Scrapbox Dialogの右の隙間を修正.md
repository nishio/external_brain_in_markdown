---
title: "✅Scrapbox Dialogの右の隙間を修正"
---

from [[✅ダイアログの見た目を改善する]]
Scrapbox Dialogの右の隙間を修正

after:
- ![image](https://gyazo.com/36c9901f53277a1f2fabebe03d133b52/thumb/1000)

before:
- ![image](https://gyazo.com/c521e80e41d01b51bdb5a7c4def5a3b2/thumb/1000)

movie:
- ![image](https://gyazo.com/24c0120e89e939636c820c8a9b2fd128/thumb/1000)

- beforeではflexのitemsの中のコンテンツにクラス名をつけて、CSSを当ててサイズをコントロールしていた
    - afterではitems自体にクラス名をつける形に変えた
    - widthで固定サイズにするのではなくflexで調節させる
- ボタンを包むdivは`flex-basis: auto;`で中身のサイズにして固定
- 入力欄のdivはbasisを固定値で入れた上でgrowで空きスペースいっぱいに広がらせる
    - 中の入力欄は外のdivのサイズに合わせる
css

```
div.input-icon {
  flex-basis: 120px;
  flex-grow: 1;
}
div.input-icon > div {
  width: 100%;
}
```

- ページタイトルは可能なら長くなって欲しくて、プロジェクト名はあまり長くなる必要がない、これはgrowの値の違いで表現している
    - これに関してはもっと良いやり方があるかも知れない

[[Flexbox]]
