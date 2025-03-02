
from [[✅ダイアログの見た目を改善する]]
Scrapbox Dialogの見た目を改善する
after:
![image](https://gyazo.com/84ce13f8e1e4073f3fdffc0da100172c/thumb/1000)

- before
    - ![image](https://gyazo.com/d01f8b60f3dfe9ca5ba2f5154044085c/thumb/1000)
- とりあえず上下にでこぼこしてるのはなんとかしたい
    - 入力欄はinputタグ直接で、ボタンはMaterial-UIなので後者に揃えるのが良さそう
        - 入力欄	[Text Field React component - Material-UI](https://material-ui.com/components/text-fields/)
- ボタンに背景色をつける
    - variant="contained" [React Button component - Material-UI](https://material-ui.com/components/buttons/)
    - ![image](https://gyazo.com/0eb4f93d2ac3c77ff0ed64b878506122/thumb/1000)
- 入力欄にこんなにパディングいらない
css

```
.MuiOutlinedInput-input {
    padding: 9px;
}
```

    - ![image](https://gyazo.com/f9a6013f0b6ea724acb2d47ef91b18be/thumb/1000)
- マージンがないせいでラベルがはみ出してるのをなおしたい
css

```
.dialog-inputs > div {
  margin-top: 7px;
}
```

    - ![image](https://gyazo.com/7856c9b750e100efade7fb5c1e37c0e3/thumb/1000)

- iPhone Xサイズだとどうなるか
    - ![image](https://gyazo.com/94bc7583e7c90ae292743e5e80c3dbdb/thumb/1000)
- サイズを調節してみる
    - ![image](https://gyazo.com/84ce13f8e1e4073f3fdffc0da100172c/thumb/1000)
        - うーん、個人的にはここが揃って欲しいけどな…
        - ![image](https://gyazo.com/c521e80e41d01b51bdb5a7c4def5a3b2/thumb/1000)
- 改善した
    - [[✅Scrapbox Dialogの右の隙間を修正]]
