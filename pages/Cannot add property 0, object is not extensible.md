
js

```javascript
foo = []
Object.freeze(foo)
foo.push(1)
// Uncaught TypeError: Cannot add property 0, object is not extensible
```

フリーズされているArrayに対してpushしようとすると起こる

具体的な発生シチュエーション
![image](https://gyazo.com/3bf53b670627bf0743ac495b6d3137d6/thumb/1000)
ではなぜフリーズされたのか？

選択された要素を[[ReactN]]に入れて、それを取り出したときにフリーズされている。うっかり破壊的更新をして厄介なバグになることを防ぐために親切な設計。

選択されたものをグループにするとき、このようなことを書いていた、これが誤り
ts

```typescript
  const group = new GroupItem();
  group.items = g.selected_items;
```

これはフリーズされたオブジェクト自体への参照を新しいグループに持たせてしまい、その後そのグループに追加をしようとした時点で上記のエラーになる

ts

```typescript
  group.items = [...g.selected_items];
```

こうすべきだった
