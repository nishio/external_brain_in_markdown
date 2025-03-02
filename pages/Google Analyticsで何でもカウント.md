---
title: "Google Analyticsで何でもカウント"
---

ある特定の操作をした人が何人いるのか知りたい。
その操作が行われた時に自分の書いたJavaScriptプログラムから直接Google Analyticsを呼び出してイベントを記録することができる。

この機能はいろいろ凝った使い方ができるが、シンプルに回数をカウントするならこれだけでいい
ts

```typescript
window.gtag("event", "harvest");
```

- harvestの部分は自分がつけたわかりやすいイベントの名前
- JavaScriptの人は`window.`がなくても動くと思う
- これがGoogle AnalyticsのEngagementのページにこう表示される
    - ![image](https://gyazo.com/0f3b5eaacb1d22186e322fc505ecf513/thumb/1000)
- そこからたどっていくと、いつどれくらい使われたかがわかる
    - ![image](https://gyazo.com/9e7c70fbee8a2144a28e47d6d1174a1d/thumb/1000)

---
詳しい話
- このgtagって関数は最初にGoogle Analyticsの設定をした時にHTMLに貼り付けるように指示されたコードの中で定義されている
- dataLayerってリストに追加しているだけ
- たぶんこのリストの中身を定期的にチェックしてサーバに送る仕組みになってるのだろう
html

```html
 <script async src="https://www.googletagmanager.com/gtag/js?id=G-GBX75RXXXX"></script>
 <script>
   window.dataLayer = window.dataLayer || [];
   function gtag() { dataLayer.push(arguments); }
   gtag('js', new Date());

   gtag('config', 'G-GBX75RXXXX');
 </script>    
```


マニュアルの記述
- 3つ目の引数で色々追加の情報を送れるようだ
- 何かを適切に設定しないといけないのかと思って混乱したが、回数をカウントするだけなら省略して良い
- [Google アナリティクスのイベントを測定する  |  ウェブ向けユニバーサル アナリティクス（gtag.js）](https://developers.google.com/analytics/devguides/collection/gtagjs/events)
js

```javascript
gtag('event', <action>, {
  'event_category': <category>,
  'event_label': <label>,
  'value': <value>
});
```

- [gtag.js API リファレンス  |  グローバル サイトタグ（gtag.js）  |  Google Developers](https://developers.google.com/gtagjs/reference/api#event)
js

```javascript
gtag('event', 'screen_view', {
  'app_name': 'myAppName',
  'screen_name': 'Home'
});
```


プロパティ追加について
- プロパティって「属性」かと思って混乱したが、Google Analytics用語としてはアカウントの直下に複数個持つことができる情報をまとめる単位のようだ
    - 新しいウェブサービスを作ったらプロパティも追加する、というイメージか
    - ![image](https://gyazo.com/a1f2e39c513892511b0f8341f133a9dd/thumb/1000)
    - ![image](https://gyazo.com/932bd389d5d9f04268c7636ebb07a06e/thumb/1000)

TypeScriptではgtagの型が不明だとエラーになるので下記のように宣言する
index.ts

```typescript
declare global {
  interface Window {
    gtag: (
      a: string,
      b: string,
      c?: { event_category?: string; event_label?: string; value?: number }
    ) => unknown;
  }
}
```


---
イベントの設定をしないといけないのかと混乱したが、しなくていいようだ
![image](https://gyazo.com/5cec00ab37f339eebab2e2eb5ca25a8a/thumb/1000)
