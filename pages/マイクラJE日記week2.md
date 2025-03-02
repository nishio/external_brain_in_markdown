
from [[マイクラJE日記]]

2021-09-19
- コンポスター
    - いらない作物を入れると骨粉になる
    - ホッパーで自動処理・自動回収できる
- ![image](https://gyazo.com/cd9b38168373f9bf388afc15d7d74058/thumb/1000)
    - 景色眺める展望タワー作ってみた
        - まったく伝わってないと思うけど正面の船着場のゲート、Mなのです
            - ![image](https://gyazo.com/e03de537931db08d844d8e00132c631b/thumb/1000)
    - ![image](https://gyazo.com/1dd8ea3ba111abcac26df1d8e9a7e663/thumb/1000)
- スキン
    - スキンを変えて遊んだことがなかったけど、みんなデフォルトではないスキンだったので僕も変えることにした
    - [https://minecraft.novaskin.me/#](https://minecraft.novaskin.me/#) で作れた
    - 特にどうしたいというこだわりがないので普段着てそうな服を着てみたw
    - ![image](https://gyazo.com/d64736b2460b59fd7b4ee6359d497d09/thumb/1000)
- 燃料不足の解決方法を調べてたらカーペットを無限増殖して燃料に使ってたw
    - [https://yotsu-cra.info/mugen-kamado](https://yotsu-cra.info/mugen-kamado)
- カボチャ
    - BEでならレール式のやつと、タワーのこれを作ったことがあるがJEでも動くかな
    - [https://kyoukura.net/automatic-melon-pumpkin-farm](https://kyoukura.net/automatic-melon-pumpkin-farm)
- JE版の農民はコンポスターから一定距離以内しか畑と認識しない

2021-09-20
- F3+Gでチャンクの境界が表示される、便利
- 手元でクリエイティブモードで実行するためにサーバのディレクトリを丸ごとZipしてMacでunzipしたら普通に動いた
- 一定時間ごとにパルスを出す仕組みについて
    - [[10倍低速ロジックアナライザ]]
    - [[ピストンループ]]
    - JEの粘着ピストンは「引き剥がし」が起きる
        - 信号が1Tの時、くっついているブロックは離し、離れてるブロックはくっつける
        - これによって1ビットの情報を保持できる
    - クロック回路をリピーターロックで止めることによって1ビットの情報を保持する仕組み
        - クロック回路がトーチとリピーターで2遅延なので2ティックの長さのシグナルが入る必要がある
            - 1ティックのシグナルを出すオブザーバーが使い勝手悪い気がする
                - 1ティックのシグナルはトーチで反転できないし
    - コンパレータは信号強度を保ったまま1ティック遅延させるのでダストで強度が下がりきって0になるまで回り続ける
        - [[コンパレータに1Tのパルスを入れると不思議な挙動]]
        - 長さNの[[コンパレータループ]]でパルス幅を延長する時、そもそもそのコンパレータループには長さN以上のパルスを入れる必要があり、それができればパルス幅を6倍に延長できる
            - 1〜4の時はリピーターで遅延させてワイヤードORで長さを2倍にできる
            - 仮にコンパレータループで40分のパルスを出そうとすると、4000個のコンパレータを並べて400秒の入力を入れる必要がある、と。
    - 20分の倍数に関しては日照センサを使えばコンパクト
- 拠点周辺がもっさりしてきたので離れたところに自分の実験場を作った
    - 植林は広い平らなスペースでやりたかったので
    - ![image](https://gyazo.com/1bbd194a0fa1bc3c5f5a49c75d30ea77/thumb/1000)

2021-09-21
- 世界に初のアンドロイド
- コマンドをホットキーにバインドするの、これでできるかと思ったが出来なかった、なぜ？
python

```
>>> import keyboard
>>> keyboard.register_hotkey("ctrl+j", keyboard.write, ("/jumpto\n", ))
```

- カボチャとスイカの自動化装置を作ってくれた
- きちんと囲ってない拠点で放置したら死んで全ロスした

2021-09-23　秋分の日
- ![image](https://gyazo.com/2e94d48d28597bb31b8c8d2dade60f9b/thumb/1000)
    - 植林とニワトリ自動化の研究をしている
- SlimefunのInfused Magnet便利
    - しゃがむと周囲のアイテムを吸い寄せる
    - 林業をやると周囲にパラパラアイテムが落ちてくるから、それの回収が楽になる
    - 自動毛刈り羊毛回収のためにInfused Hopperを作ろうと思ってその素材として作ったんだけど、普通のホッパーで現状は十分
        - 6個ホッパーを引いて感圧板を真ん中に置くスタイル
- 深い穴に落ちて死んだので愚痴ってたらスライムブーツをもらった。SlimefunのMagic Armer
    - ジャンプ強化、落下ダメージ無効、これは便利
    - 6マスジャンプできる
- ニワトリ装置が完成した
    - ![image](https://gyazo.com/fa230997a34f9f7c79d1e4c643fb1221/thumb/1000)
    - [[マイクラのニワトリ]]
- 6時間経験値トラップに放置したらレベル140になってた
    - 1時間で1万Expくらいだしている。167EXP/分なので3〜4秒に一回、10EXPのブレイズを倒してると考えれば妥当。
    - サボテンかまどは6EXP/分なので桁違い。ユーザがその場にいなくても蓄積していくのが長所だが、燃料がなかった間のサボテンがチェストに入り切らなくて溢れて消えたりしてる。人間の側の需要に波があるから難しいなぁ。焼いたものではなく経験値が欲しいからかまどを大量に並列で並べて一気に焼くわけにもいかないし(経験値の回収は一つずつやることになる)
    - やっぱりこまめにトラップに行くのが正解かな、計算が正しければ30分でレベル50になる

- うわっ、ラージチェスト5杯ものブレイズロッドが溜まってるw
- バッテリーができないと思ったらCopper Ingotという名前のオブジェクトは本家とSFと2種類あるのか…
- ダイヤのブーツとレギンスを売る防具職人、てっきりその二種類しか売らないのだと勘違いして2人目を育ててしまったけど、JEではその上のレベルで上半身の装備を売るのね…
- GPS GEOスキャナーを作ったがこれだけあっても機能しないのか…
    - GPS衛星のネットワークを十分発展させるか、衛星を打ち上げないですぐそばで使うかの二択かな

- Iron Dustが不足
    - GEO Miner、鉱石が手に入りそう
        - →ウランとか取るやつ
    - 高度な採掘機なら鉱石ブロックのまま取れる
        - 鉱石ブロックからは二個のダストが手に入る
        - 幸運のツルハシで採掘する？幸運3でも2倍になるだけなので鉱石ブロックのまますりおろすのと変わらない、手間がない分鉱石ブロックのままやる方がいい
            - スイカの収穫に幸運の効果が掛かるの初めて知った
    - 鉄インゴットから粉末にできるならゴーレムトラップという経路があるのだが…
        - > Additionally, crushing an Iron Ingot in an Electric Ingot Pulverizer produces one piece of Iron Dust.
            - インゴットから作れるじゃん
    - /shopコマンドでゴーレムスポナーを買う案
        - $1,000,000貯めればshopでアイアンゴーレムスポナーを買える
        - デフォルトの設定のままなのだがopでないと購入できない状態だった
            - ![image](https://gyazo.com/22f7511c0c588c509163172a89d559ed/thumb/1000)
            - どこの設定を直すべきなのかわからない
                - わかった see [[EconomyShopGUI]]
        - 何を売るかは悩ましい
            - 緑の染料、3セント　ラージチェストいっぱい売っても100ドル程度
            - ブレイズロッド　ラージチェスト231.5個分
            - レンガブロックが23ドルもするな
                - (余りまくってた粘土を村人に売ってしまった後だが)
            - ブレイズロッド1.25ドルよりウール7ドルの方が高い
                - 2126スタック…

- ゴーレムトラップ
    - JEとBEでゴーレムのスポーン条件はだいぶ違う
        - [Tutorials/Iron golem farming – Official Minecraft Wiki](https://minecraft.fandom.com/wiki/Tutorials/Iron_golem_farming)
        - ![image](https://gyazo.com/4fc56a4d5e9058b4055c623a05c943df/thumb/1000)
            - [https://zenzenzenchan.com/minecraft-iron-golem-farm-new-version/](https://zenzenzenchan.com/minecraft-iron-golem-farm-new-version/)
        - JEのゴーレムトラップは「村から100マス離れろ」とか言われないのね
    - ゴーレムトラップ、溶岩の中でもがいてるゴーレムを殴れば倒した判定になるのでSlimefunのアイテムもドロップする


2021-09-24
- dynmapはチャンクごとにローカルのファイルシステムに画像を出力しているのでこれを繋ぎ合わせて1枚の画像にすることができそう
- 指定範囲の再レンダリングをコマンドでできるので早朝にcronでやるのも手かも
- Transport Pipe、しゃがんでレンチをパイプ側面をクリックするとその方向への接続をオンオフできる
    - ユーザごとのレンダリング設定がある
        - 一人だけ設定がVANILLAに変わってた、他の人はMODELLED
        - 一人だけパイプが表示されない問題が発生していたがおそらくこれが原因
- ゴーレムトラップ、一晩放置したけどうまく流れてなくて1スタックしか取れてなかった
    - これで村の道具鍛冶も育てられるな、無限ダイヤ道具の時代
    - アクセスが悪すぎるので将来的にゴーレムスポナーが手に入ったらメイン拠点に置くのもいいかもね、使うのはそこだし
- ダイヤの武器、防具、道具、すべて村人から買えるようになりました
- 成果物をパイプで吸い出すと溶岩バケツのバケツは残ってしまう

- パイプ爆発デモ
    - [https://scrapbox.io/files/614d5ad0389df0001d103e8b.mp4](https://scrapbox.io/files/614d5ad0389df0001d103e8b.mp4)
    - 一定以上のアイテムがパイプに入ると爆発する
        - デフォルトでは20
        - デフォルトの1個流しなら発生せず、オプションをいじるとパイプの構造によっては発生する、というバランス

2021-09-25
- dynmapをcronでトリガーすることにした
    - 毎日朝6時にdynmapで拠点周辺の再レンダリングをするようにしました
    - ![image](https://gyazo.com/4858b793f6c736e6027476859560e585/thumb/1000)
    - ![image](https://gyazo.com/e4dcfef99c12edd58d9953749f13d679/thumb/1000)
- [[dynmapのタイルを繋ぎ合わせて大きな画像をつくる]]

2021-09-26
うすうす分かってはいたがTier1のGPS Transmitterでは1つではGEOスキャンできないのな…
- Tier2のを作ってY=125におけばギリ足りる、GPS衛星はやはり高いところに必要ということか
java

```
public int getMultiplier(int y) {
    return y * 4 + 100;
}
```

- [src](https://github.com/Slimefun/Slimefun4/blob/master/src/main/java/io/github/thebusybiscuit/slimefun4/implementation/setup/SlimefunItemSetup.java#L1846)
- その後Tier2を作るのにTier1が4つ必要だとわかって、結局Tier1を高度200に3つ設置した

Programmable Androidできたー！！
- ![image](https://gyazo.com/e62323a046207ecce1de3d9060822a49/thumb/1000)

黒曜石だろうと容赦なく1秒で採掘する、重力の影響を受けない、進む先が溶岩だったら進まずに停止する、賢い！そして人間が賢くない。
- [https://scrapbox.io/files/614f531e398a2f002270013b.mp4](https://scrapbox.io/files/614f531e398a2f002270013b.mp4)
- 安心してください、少しこれは並行世界です。生まれて早々に溶岩に沈んだアンドロイドはいません！

毎秒1個の丸石を得る地味な労働に従事しています
![image](https://gyazo.com/16fd8d06e0b1f343fa592d91d31bdef7/thumb/1000)

![image](https://gyazo.com/421282cca9dbe33e2b6735d6bdb2c1b7/thumb/1000)
- 世の中的にはそういう認識なのか…
- 僕は条件分岐がしたい！
- [ここ](https://github.com/Slimefun/Slimefun4/blob/master/src/main/java/io/github/thebusybiscuit/slimefun4/implementation/items/androids/ProgrammableAndroid.java#L700)でプログラムカウンタを1増やしてインストラクションを取得して実行、って繰り返してるだけなので、条件によってプログラムカウンタを操作する命令を追加すれば…(まてまて
- Maven
    - [https://maven.apache.org/install.html](https://maven.apache.org/install.html)
    - ![image](https://gyazo.com/260586b2c7fb45cadca4cb32e334853e/thumb/1000)
    - とりあえずビルドすることはできたw
- 独自コマンドの追加ができた
    - ![image](https://gyazo.com/b1d49674344f53f5c3cee549e8f67a12/thumb/1000)
- オリジナルの言語仕様がオペランドを取らない命令の羅列なのでここから拡張していくのは(不可能ではないが)足場が悪いなーと思っている
- エラーを起こしてアンドロイドが消えたww
    - バグのあるプログラムを書くとアンドロイドが死ぬ開発環境、ハードル高すぎww
:

```
[12:15:42 ERROR]: [Slimefun] X: -56 Y: 63 Z: -239 (PROGRAMMABLE_ANDROID_MINER)
[12:15:42 ERROR]: [Slimefun] has thrown 4 error messages in the last 4 Ticks, the Block has been terminated.
```

    - `ImportError: Cannot import site module and its dependencies: No module named site`
        - jython、普通のバージョンはライブラリが別ファイルになってて、それらを適切な場所に置く必要がある。全部入りのjython-standaloneが別途ある
- Minecraft(PaperMC+Slimefun)のProgrammable AndroidのなかでPythonが実行できるようになった！
    - ![image](https://gyazo.com/3c2874d8a7d6c3b3609124bdf9744f58/thumb/1000)
    - Programmable Androidをまともな言語でプログラミングできるようにしたけど、マイクラGUI上でプログラミングするのはまともな開発環境ではないので、まともにVSCodeとかで開発してGithubにpushしたらマイクラ世界のロボットの挙動が変わって欲しいですね(待て

2021-09-27
- [https://github.com/ammaraskar/pyCraft](https://github.com/ammaraskar/pyCraft)
    - > Minecraft-client networking library in Python.
- 「Minecraftは、ボクセルのWebになる」 [PDF](https://github.com/kengonakajima/blog/blob/master/articles/minecraft_web.pdf)
- [wiki.vg](https://wiki.vg/Main_Page)
- [https://prismarine.js.org/](https://prismarine.js.org/)
    - `server.properties`で`online-mode=false`すればMojangの認証なしでボットアカウントでログインできる
    - しかしtrueだった時代とユーザデータが変わり、持ち物や進捗、Slimefunの研究などがリセットされる
    - それは許容できないのでいったん戻した

:

```
[03:51:18] [Craft Scheduler Thread - 243 - DriveBackupV2/INFO]: [DriveBackupV2] Uploading file to Dropbox
[03:51:28] [Craft Scheduler Thread - 243 - DriveBackupV2/INFO]: [java.net.SocketException: Connection reset by peer, java.net.SocketException: Connection reset by peer]
[03:51:28] [Craft Scheduler Thread - 243 - DriveBackupV2/WARN]: java.net.SocketException: Network is unreachable
```



[https://github.com/PrismarineJS/mineflayer](https://github.com/PrismarineJS/mineflayer)
`Error: This user does not have any items on its accounts according to minecraft services.`
- 自分のアカウントで同時に2つログインはできないので別のMSアカウントを作った
- しかしそのアカウントでは未購入だからプレイできない
    - 買った
![image](https://gyazo.com/9e9d48a20ead33c57df3d42ce99ca29f/thumb/1000)


[https://github.com/PrismarineJS/mineflayer-pathfinder](https://github.com/PrismarineJS/mineflayer-pathfinder)


[https://scrapbox.io/files/61516cc5934d12001d0dc045.mp4](https://scrapbox.io/files/61516cc5934d12001d0dc045.mp4)

[https://scrapbox.io/files/61517e27f11b61001db4a93b.mp4](https://scrapbox.io/files/61517e27f11b61001db4a93b.mp4)

![image](https://gyazo.com/b1796cf62428d8b53723376c35274beb/thumb/1000)



![image](https://gyazo.com/25774d0815d3c12ca08229f1cc8a485b/thumb/1000)
![image](https://gyazo.com/e23e7109fc90dfb2e5df389dc392f48b/thumb/1000)

![image](https://gyazo.com/71fa6273e7c7459ab2710ac4356b5789/thumb/1000)
[https://scrapbox.io/files/6152987f2c636e001dcaadf6.mp4](https://scrapbox.io/files/6152987f2c636e001dcaadf6.mp4)

![image](https://gyazo.com/0e26236c02593225e085385c87518d3d/thumb/1000)


![image](https://gyazo.com/d09ffc2f2f11afee262c6dadeb550175/thumb/1000)

[https://twitter.com/nishio/status/1443221023667605513](https://twitter.com/nishio/status/1443221023667605513)


![image](https://gyazo.com/4d09c1ee6255bcf413a891f2004beffb/thumb/1000)
![image](https://gyazo.com/e1a3d8df97927087d14674b439058d52/thumb/1000)
![image](https://gyazo.com/6bfed79898da4ab4bdfac7299d9dd6fe/thumb/1000)

[https://minecraft.fandom.com/wiki/Head](https://minecraft.fandom.com/wiki/Head)

[https://minecraft.fandom.com/wiki/Tutorials/Amethyst_farming](https://minecraft.fandom.com/wiki/Tutorials/Amethyst_farming)

[https://youtu.be/eYmUBfXan9Y](https://youtu.be/eYmUBfXan9Y)

[https://minecraft.fandom.com/wiki/Air](https://minecraft.fandom.com/wiki/Air)

[https://github.com/kii-chan-reloaded/GeneticChickengineering](https://github.com/kii-chan-reloaded/GeneticChickengineering)

[https://github.com/Sefiraat/EMC2](https://github.com/Sefiraat/EMC2)

[[マイクラ]]
