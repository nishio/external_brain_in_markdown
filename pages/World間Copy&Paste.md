
World間Copy&Pasteできた
![image](https://gyazo.com/9232a70499465d09800a27f8530e336b/thumb/1000)
copy元
- [Tokyo Skytree, tallest tower in Japan. HQ !! Minecraft Map](https://www.planetminecraft.com/project/tokyo-skytree-tallest-tower-in-japan-hq-/)
- ![image](https://gyazo.com/0d022853f06d0cad125817c0393f91e4/thumb/1000)
遠景
- ![image](https://gyazo.com/6cd6cb3cf14f85e46ca4d52043648371/thumb/1000)

残念ながら先端のアンテナは壊れてる
たぶんオリジナルはY=64より低いフラット地面から高度上限のY=256まで使って作られてて、それをこちらは普通のマップのY=64に設置したから無くなってしまったのだと思う。
- >  The tower is almost 250 blocks-tall, that is close to the maximum height.
    - やはりそう

これは悩ましい、マイクラのブロックで「一回り小さくする」はやりづらい

how to
- [[ストラクチャーブロック＠マイクラ]]を使おうと考えたがJEでは48×48×48が最大サイズだった
- [[WorldEdit]]を使う
    - > WorldEdit can work with “schematic” files to save or load your clipboard to disk.
    - >  To save your current clipboard to file, use `//schem save <filename>`.
    - >  To load a saved schematic, use `//schem load <filename>`.
    - [https://worldedit.enginehub.org/en/latest/usage/clipboard/](https://worldedit.enginehub.org/en/latest/usage/clipboard/)
- やったこと
    - ローカルでサーバ起動
        - プラグインにWorldEditが入ってる
        - worldを上記の配布ワールドで置き換え
    - コピーしたい範囲を`//wand`の杖で選択して`//copy -e`, `//schem save <name>`する
        - ファイルは`minecraft_server/plugins/WorldEdit/schematics/<name>.schem`って感じで生成される
    - このファイルをペーストしたいマルチプレイサーバの同様のパスに置く
        - `//sheme load <name>`,  `//paste`する

注意点
- 自分から見てどの方向にペーストされるのかF3でコピー時の方向を見てメモっておくべき
    - それを怠ってペーストして、既存のものに上書きしてしまった
    - `//undo`でブロック自体は復元できるが、この時に壊したのがSlimefun4の機能で作ったテレポーターで、ブロックだけ復元しても元通りには機能しないので作り直しが必要だった

[[マイクラ]]