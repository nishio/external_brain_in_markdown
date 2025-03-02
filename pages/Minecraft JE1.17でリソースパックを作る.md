---
title: "Minecraft JE1.17でリソースパックを作る"
---

![image](https://gyazo.com/ce90a54c8ec00d03eb7769caf37d3428/thumb/1000)

まとめ
- 既存のモデルのテクスチャを変えるのは楽
    - 画像を変えるだけなので。
- 鎧兜などのデザインを変えるのも簡単
    - モデルのテクスチャを変えることしかできない
    - なのでテクスチャ変更同様の難易度
    - [[Blockbench]]を使うことがおすすめ
        - 新規作成のMinecraft SkinからArmorとかを選んで3D形状を見ながら塗り絵ができる
        - ![image](https://gyazo.com/49b00262720f1a0afba7fbd8078fe2cc/thumb/1000)
        - Armor編: [[Minecraft JE1.17でリソースパックを作るArmor編]]
- ブロックの形状を変えるのは難しい、色々な仕様が影響して複雑
    - 当たり判定のない物でよいなら、手持ちのアイテムとして作り額縁に入れるのが良い
    - 下記のカスタム例は全部額縁に入ったアイテム(額縁のモデルを1/4に縮小している)
        - ![image](https://gyazo.com/ea16067f3656b52bf69eeed8262343f4/thumb/1000)![image](https://gyazo.com/4d8ccf80f89415d429453c114f5e5de7/thumb/1000)![image](https://gyazo.com/9dd7207a3b0e3af21215aaee67518cd9/thumb/1000)

    - Block編: [[Minecraft JE1.17でリソースパックを作るBlock編]]


---
以下Texture編
- Armor編: [[Minecraft JE1.17でリソースパックを作るArmor編]]
- Block編: [[Minecraft JE1.17でリソースパックを作るBlock編]]

---
[チュートリアル/リソースパックの作成 - Minecraft Wiki](https://minecraft.fandom.com/ja/wiki/チュートリアル/リソースパックの作成)
を読んだがわからない

[https://www.youtube.com/watch?v=kp5iCZxEmt4](https://www.youtube.com/watch?v=kp5iCZxEmt4)
これをみたらわかった
まず[.minecraft - Minecraft Wiki](https://minecraft.fandom.com/ja/wiki/.minecraft)でマイクラのファイルの位置を確認
- `Mac OS X	~/Library/Application Support/minecraft`
- そしてminecraft/versionsのjarをzipにして展開する
- assetsに色々なファイルが入っている

中を見てみよう
assets/minecraft/blockstates/blue_terracotta.json

```json
{
  "variants": {
    "": {
      "model": "minecraft:block/blue_terracotta"
    }
  }
}
```


assets/minecraft/models/block/blue_terracotta.json

```json
{
  "parent": "minecraft:block/cube_all",
  "textures": {
    "all": "minecraft:block/blue_terracotta"
  }
}
```

つまり形状がキューブで全面のテクスチャが同じであり、そのテクスチャは`block/blue_terracotta`

ところでここまできてから気づいたけど`blue_terracotta`は単色のやつで、僕が探してたのは`blue_glazed_terracotta`だった
`assets/minecraft/textures/block/blue_glazed_terracotta.png`
- ![image](https://gyazo.com/7e633a24906f59778fdfc625fe5cfa55/thumb/1000)
- ![image](https://gyazo.com/331de1bb1118dddf092d2514d79e1bcb/thumb/1000)
- これを別の画像で置き換えてみる

あらためて、今から作ろうとしているものが黄色いことを思い出したので`yellow_glazed_terracotta`を見る
assets/minecraft/blockstates/yellow_glazed_terracotta.json

```json
{
  "variants": {
    "facing=east": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 270
    },
    "facing=north": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 180
    },
    "facing=south": {
      "model": "minecraft:block/yellow_glazed_terracotta"
    },
    "facing=west": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 90
    }
  }
}
```

これはブロックの向きの情報によって表示するモデルをY軸周りに回転せよ、という指令

で、そのモデルはこう
assets/minecraft/models/block/yellow_glazed_terracotta.json

```json
{
  "parent": "minecraft:block/template_glazed_terracotta",
  "textures": {
    "pattern": "minecraft:block/yellow_glazed_terracotta"
  }
}
```


`assets/minecraft/textures/block/yellow_glazed_terracotta.png`
結論、この画像を差し替えれば良いはず

このassetと同じディレクトリ構造で差し替えるファイルだけを.minecraft/resourcepacks以下におけば良い

作ったリソースパックを入れる
![image](https://gyazo.com/3a6ab9a0a9dc4611cb60294460772654/thumb/1000)

![image](https://gyazo.com/80ff9a4badcdd1219a74150f382216ab/thumb/1000)
できた

加筆
![image](https://gyazo.com/f159cb7954c614ab89a8aaeadca8a851/thumb/1000)
という構造なのでX.pngを直接置き換えるか、新しいファイルを置いてblock/X.jsonからの参照を書き換えると良い
- そうすれば手持ちのアイテムのモデルも書き換えたものになる
![image](https://gyazo.com/ce90a54c8ec00d03eb7769caf37d3428/thumb/1000)


assets/minecraft/models/item/yellow_glazed_terracotta.json

```json
{
  "parent": "minecraft:block/yellow_glazed_terracotta"
}
```

assets/minecraft/models/block/yellow_glazed_terracotta.json

```json
{
  "parent": "minecraft:block/template_glazed_terracotta",
  "textures": {
    "pattern": "minecraft:block/yellow_glazed_terracotta"
  }
}
```

assets/minecraft/blockstates/yellow_glazed_terracotta.json

```json
{
  "variants": {
    "facing=east": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 270
    },
    "facing=north": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 180
    },
    "facing=south": {
      "model": "minecraft:block/yellow_glazed_terracotta"
    },
    "facing=west": {
      "model": "minecraft:block/yellow_glazed_terracotta",
      "y": 90
    }
  }
}
```



次にこれをサーバに置いて、参加者がリソースパックの設定をしなくても適用されるようにする
- [[サーバリソースパック試行錯誤ログ]]

今は僕の手元(Mac)で下記のシェルスクリプトを実行している
resourcepacks/cybozu/build.sh

```
zip -r ../cybozu.zip .
shasum ../cybozu.zip
mv ../cybozu.zip ~/Dropbox
```

表示されたハッシュ値をserver.propertiesに書き、サーバを再起動する。
サーバの設定はこんな感じ
server.properties

```
resource-pack=https\://www.dropbox.com/.../cybozu.zip?dl\=1
require-resource-pack=true
resource-pack-sha1=...
```


クライアントは再度ログインした後、サーバリソースパックを受け入れるか質問される
- 受け入れて進むとダウンロードされるかと思いきや、されない、なぜ？
- その次に接続したときにダウンロードされる
