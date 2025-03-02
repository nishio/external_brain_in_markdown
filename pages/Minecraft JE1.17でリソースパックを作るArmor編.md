---
title: "Minecraft JE1.17でリソースパックを作るArmor編"
---

まとめ
- アーマーのモデルは変更できない
- アーマーのテクスチャー画像を編集するだけ
    - 画像を倍のサイズにするなどして解像度を上げることはできる
- [[Blockbench]]を使うことがおすすめ
    - 新規作成のMinecraft SkinからArmorとかを選んで3D形状を見ながら塗り絵ができる
    - ![image](https://gyazo.com/ba7daafdd8e632a6072b1fcef8f884a7/thumb/1000)
---
アーマーのモデルは変更できない
アーマーのテクスチャー画像を編集するだけ
`assets/minecraft/textures/models/armor/iron_layer_1.png`
- ![image](https://gyazo.com/998aaf77c03ee5c76b1a6e2689568b5e/thumb/1000)

:assets/minecraft/models/item/iron_chestplate.json

```json
{
  "parent": "minecraft:item/generated",
  "textures": {
    "layer0": "cybozu:item/iron_chestplate"
  }
}
```


出来上がった物をマネキンに着せてみる
![image](https://gyazo.com/2463814b1b53125e4c9d6f94570dfac0/thumb/1000)


![image](https://gyazo.com/c0ee6689dcd495dce59d3310ae91e7c5/thumb/1000)

---
Blockbench
![image](https://gyazo.com/ba7daafdd8e632a6072b1fcef8f884a7/thumb/1000)
3Dを見ながら作業できるから格段に楽だわ
![image](https://gyazo.com/49b00262720f1a0afba7fbd8078fe2cc/thumb/1000)

