
まとめ
- ブロックの形状を変えるのは難しい
    - 色々な仕様が影響して複雑
        - 周辺ブロックの面カリング、向きの有無、照明に対する影響、など
    - 当たり判定のない物でよいなら、手持ちのアイテムとして作り額縁に入れるのが良い
        - ただし、上に立てない、物を乗せたりもできない
        - 例:
            - ![image](https://gyazo.com/f6a27ae86f21dc4eb021e61dca6c03b0/thumb/1000)



---試行錯誤ログ
![image](https://gyazo.com/fb204414fc85b8e822aca3dba10445f5/thumb/1000)

実際のブロックがある位置から上下左右1マスの3×3×3の範囲に直方体を置くことができる
- 「高さ3にできる」と思い込んでて「あれ？伸ばせないな？」と思ったが下に1マス上に1マスで高さ3になる
- 直方体は22.5度の倍数でのみ回転できる
- 元が立方体であるモデルを差し替えた場合、表示がおかしくなる
    - キリン(?)の足元の地面が消えている
    - これはおそらくブロックが隣接している時に隣接面を描画しない最適化が入っているのだろう

![image](https://gyazo.com/01d14822b4a4315f290cb4d31805e87a/thumb/1000)
- (いいタイミングでクリーパーが来たからF2連打したのだがチャット欄が映ってしまった)
- ブロックを宙に浮かせて他のブロックと隣接させないことで見た目をまともにすることはできた
- ただし現状は元々のブロックの位置に当たり判定と影の表示面があるので上に乗ると変
    - 制御する方法はあるはずだが…
        - Discordできいたとこによるとないらしい

> ブロックが隣接している時に隣接面を描画しない最適化
assets/minecraft/models/block/cube.json

```json
{
   "parent": "block/block",
   "elements": [
       {   "from": [ 0, 0, 0 ],
           "to": [ 16, 16, 16 ],
           "faces": {
               "down":  { "texture": "#down", "cullface": "down" },
               "up":    { "texture": "#up", "cullface": "up" },
               "north": { "texture": "#north", "cullface": "north" },
               "south": { "texture": "#south", "cullface": "south" },
               "west":  { "texture": "#west", "cullface": "west" },
               "east":  { "texture": "#east", "cullface": "east" }
           }
       }
   ]
}
```


Discordで聞いたこの問題を解決するための方法
- 他のブロックのcullfaceを発動しないモデルをベースにする
- 不可視のアーマースタンドのヘッドスロットに入れる
- 不可視のフレームに入れる

他のブロックのcullfaceを発動しないモデル
- ガラス、感圧板、花など
- 花は木材ブロックの上に置けないからガラスか感圧版か…他に何があるのかな？
- 何が発動しないのかのリストなどはないようだ
- lecternも下の面を消してしまう
    - どのオブジェクトが隣の面を消すかはハードコードされてるっぽい？

ガラスを置き換えてしまうのは微妙なので感圧板かな…
- とか考えるとどのオブジェクトを潰すかとか振る舞いがどうかとか考えるのめんどくさいからMODでオブジェクトを追加しようぜとなるのがよくわかって来た
- 限られた枠しかないのが面倒だな

ブロックと違ってアイテムはパラメータによるモデルの切り替えがある
- なんでブロックにないんだよ…
- なのでアイテムとして作ってワールドに配置する時には不可視のフレームを使うという手がある
    - これなら枠は無尽蔵になる
    - しかしまあ、フレームはブロックにくっついてしか存在できないので…うーむ

まあ一番マシそうな感圧版にしておくか
- うーわ、感圧版には「置かれた向き」の属性がないので一定の向きにしか置けない
- ![image](https://gyazo.com/044628ff5bc595c784fa338c266de4c3/thumb/1000)

あと、すごい持ち方してるなw
- ![image](https://gyazo.com/a99f24c058312fdf4a14f14f29be5458/thumb/1000)

[https://www.youtube.com/watch?v=aaJ8XgMAOno](https://www.youtube.com/watch?v=aaJ8XgMAOno)
Itemにすることにした

持ち方は[[Blockbench]]の右上の「Display」から変更できる。
- 本当はこんな持ち方をすると指の力がものすごく必要なのだが、腕を掲げて待つ機能がないので仕方ない。両手で持つと膝で蹴りながら歩いてしまう
- ![image](https://gyazo.com/fc1b39e9d7bf910b08a69551deb9ffb2/thumb/1000)

額縁に入れた時の見た目も調整する
![image](https://gyazo.com/e8b8b41b49bcfdd9524e23630647b5a5/thumb/1000)

やっと許容できる見た目になった
- ![image](https://gyazo.com/f6a27ae86f21dc4eb021e61dca6c03b0/thumb/1000)
- 奥にある小さいマウスパッドのようなものが1/2サイズに縮小した額縁
    - 不可視にするという案があったが見えないものがあるのはそれはそれで罠になりそうだから物を置いた時に隠れるサイズにしてみた
    - 額縁に入れた物は、入れた後で45度ずつ回転できる
    - MacBook自体はブロックではなくアイテムにした(石の斧)

石の斧などの既存のモデルを直接書き換えるのではなく、macbook.jsonを継承させている。
- Blockbenchで編集する場合に「 MacBookを編集したいからmacbook.jsonを開く」となって自然
    - 「えーと、MacBookは石の斧だから…」みたいなのは良くない
cybozu/assets/minecraft/models/item/stone_axe.json

```json
{
  "parent": "item/macbook"
}
```


- Q: 参照を`"minecraft:item/macbook"`や`"cybozu:item/macbook"`にしなくて良いのか？
    - A: 今のところそれで問題なく動いている
        - 複数のリソースパックが混在するときには、意図しない干渉を防ぐために名前空間を分けるとよい
        - 今回のケースではこのリソースパックを再配布するわけではなく、むしろ1つのパックにまとめた上でサーバリソースパックとする、だから内部で名前空間分けてもめんどくさいだけ

透明テーブル
- ![image](https://gyazo.com/18c3cc10a2fe794141708d0d59904e06/thumb/1000)
- 最初cobblestoneを置き換えたが、天板が透明にならなかった
    - glassを置き換えたら透明になった
    - テスクチャの透明度を考慮するかどうかのフラグがあると見える

Minecraftに座れる丸椅子を導入するにはどうすればいいか
- GSitで座れるのはブロックだけ
- ブロックのモデルをリソースパックで置き換えても隣接ブロックの面のカリングが発生して見栄えがおかしくなる
- 実際のオブジェクトと表示位置をずらすのは当たり判定の位置を変更できないのでダメ
- 解
    - 床材を限定する
    - 床材の上面のカリングをオフにすれば上にブロックを乗せても大丈夫
    - まずオフィスの床っぽい素材を作って、それを引いたところだけ椅子が置ける
- 別解
    - ブロックの基底モデルを変更して上面のカリングをオフにする
    - しかしこれは地中のブロック全ての上面がレンダリングされる
- 追記
    - 最終的に照明との兼ね合いで「ハーフブロックの上付き時のモデルを置き換え」という結論になった

床材限定の試行錯誤:
天然に存在しないコンクリートブロック、parentで全面カリングのあるcube_allを参照しているが、ここを差し替える
assets/minecraft/models/block/gray_concrete.json

```json
{
  "parent": "minecraft:block/cube_all",
  "textures": {
    "all": "minecraft:block/gray_concrete"
  }
}
```


上面のカリングを行わないブロック
json

```json
{
  "parent": "block/block",
  "elements": [
    {
      "from": [0, 0, 0],
      "to": [16, 16, 16],
      "faces": {
        "down": { "texture": "#all", "cullface": "down" },
        "up": { "texture": "#all" },
        "north": { "texture": "#all", "cullface": "north" },
        "south": { "texture": "#all", "cullface": "south" },
        "west": { "texture": "#all", "cullface": "west" },
        "east": { "texture": "#all", "cullface": "east" }
      }
    }
  ],
  "textures": {
    "particle": "#all"
  }
}
```


右や左の椅子では足元に穴が空いてるが、コンクリートの上に置かれた真ん中の椅子では大丈夫
![image](https://gyazo.com/2dbb6fbc9512d31a81300cb62f0dbe35/thumb/1000)
だが、なんか色が違うな…
- あっ、そうか、ブロックと隣接してる扱いだから照明が0なのか！
- 上付きスラブなら足元が暗くならない
- ![image](https://gyazo.com/7e48e11b5a4e971a7368b9a319a95c50/thumb/1000)


![image](https://gyazo.com/a9568e02e7146f87f7aa19236f210969/thumb/1000)
![image](https://gyazo.com/29ad883c9626a0252ab290d04fba3a30/thumb/1000)

ローカルのリソースパックのファイルを更新してF3+Tでリロードしてテストし、完成したらzipでまとめてサーバリソースパックにする、という開発フローを取っている
- サーバリソースパックの更新プロセス
    - 設定ファイルを書き換える
    - サーバを再起動する
    - クライアントが接続し直すと「サーバリソースパックを受け入れるか？」と聞かれる
    - Proceedを選ぶがここではリソースパックがロードされない(え？)
    - 次に接続したときにリソースパックのダウンロードと適用が行われる(なんでだよ)

![image](https://gyazo.com/51059e841f25cd90ec23016ec290a156/thumb/1000)
元ネタ
![image](https://gyazo.com/d9ec23684a555ac1a7ea64b7fbafc747/thumb/1000)
[カフェにBARに公園も！ サイボウズの日本橋オフィスが実用性と居心地を見事に兼ね備えていてすごい | サイボウズ式](https://cybozushiki.cybozu.co.jp/articles/m001002.html)
- 組み合わせて使えるように設計したから贅沢に3画面使って作業できます
- ![image](https://gyazo.com/4d8ccf80f89415d429453c114f5e5de7/thumb/1000)
- テクスチャを作るのが面倒という理由でキーボードは全員HHKB無刻印

[https://twitter.com/nishio/status/1447569969806405643?s=20](https://twitter.com/nishio/status/1447569969806405643?s=20)

[https://twitter.com/nishio/status/1447585160761798666?s=20](https://twitter.com/nishio/status/1447585160761798666?s=20)

[https://twitter.com/nishio/status/1448145564302860297](https://twitter.com/nishio/status/1448145564302860297)
