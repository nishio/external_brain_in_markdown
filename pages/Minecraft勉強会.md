---
title: "Minecraft勉強会"
---

「Minecraftは、ボクセルのWebになる」 [PDF](https://github.com/kengonakajima/blog/blob/master/articles/minecraft_web.pdf)
- 2021-09-08 「オンラインゲームを支える技術」の中嶋 謙互さんによるスライド
- この解釈に西尾も賛成、それに加えて
    - Minecraftはそもそも
        - 3Dバーチャル空間で
        - コラボレーションできる
        - プラットフォーム
    - 物理オフィスのバーチャル化を考える上で無視できない
    - 良い特徴: ユーザが場を改善するコストが安い
        - kintoneによって「社員が誰でも業務アプリを作成・改善できる」が実現されたように
        - Minecraft上のバーチャルオフィスは社員の誰でもが作成・改善できる

Minecraftの2021年現在のエコシステム
- まずこれを解説する
- バニラ
    - 公式のオリジナルリリースのこと(一般名詞)

- MOD(MODサーバ/MODクライアント)
    - 初期に作られた、今でも開発が継続しているものもある(例: [Forge](https://files.minecraftforge.net/net/minecraftforge/forge/))
    - サーバとクライアントを改造したもの
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ドキュメントもソースコードもなしによくやるよな
    - MojangはMOD作者を雇用してMOD作成を容易にするAPIの開発をした
    - クライアントとサーバのMODのバージョンを合わせる必要がある

- この後に2つ重要な要素が生まれた
    - [SpigotMC](https://www.spigotmc.org/wiki/about-spigot/)
        - 2012年
            - 無料/オープンソースを標榜するMOD作者&ユーザのコミュニティ
            - メンバーは30万人以上
        - 知識の共有が行われるようになった
    - バニラクライアントでの利用が可能になった
        - ![image](https://gyazo.com/5841196691409c19e1603c045517e672/thumb/1000)

- なぜバニラクライアントでの利用が可能になったか？
    - バニラに追加された「リソースパック」機能
        - クライアント側のプログラムを変更することなく、モデルやテクスチャを追加変更して新しい見た目を作ることができる
    - バニラのクライアントで追加機能GUIを作るノウハウの蓄積(後述)

- バニラクライアントで利用できる、つまり
    - サーバごとに異なるソフトウェア(MODクライアント)を使うことなく、
    - 単一のソフトウェア(バニラクライアント)でサービスを受けられる
- これってWebの
    - サーバごとに異なるソフトウェアを使うことなく、
    - 単一のソフトウェア(インターネットブラウザ)でサービスが受けられる
- と同じ状況が生まれたわけだ
- Web技術に例えると
    - Common Gateway Interface(CGI)が発明されて、
    - サーバ側でプログラムを実行して
    - 静的なコンテンツ配信ではなく、動的な振る舞いの変更が可能になった
    - これがMinecraftにおいてプラグインAPIの整備によって起こったこと
    - (細かいことを言えば別プロセスを起動するのではなく、サーバと同一プロセス内で動くのでmod_perlが生まれた後ぐらいの状況)
    - APIさえ守っていればサーバ側の実装は取り替えられる
        - ApacheをNginxにするみたいに。
        - これがMinecraftにおいても発生
            - 今はSpigotより性能を改善したという触れ込みのPaperMC/Paperが主流
            - [PaperMC/Paper: High performance Spigot fork that aims to fix gameplay and mechanics inconsistencies](https://github.com/PaperMC/Paper)

- というわけで「Minecraftは、ボクセルのWebになる」
    - 技術的には既にその状態
    - Minecraftがデファクトスタンダードになるかどうかはブラウザのシェア争いと同じ
        - 技術と違うレイヤー
    - Minecraftって今どこの会社が持ってるんだっけ
        - 2014年09月17日 [ASCII.jp：マインクラフト買収はマイクロソフトの「防衛策」](https://ascii.jp/elem/000/000/933/933106/)
        - > マイクロソフトは、マインクラフトが生みだすエコシステムを欲したとも思われる。
        - >  マインクラフトは単なるゲームではなく、クラウド型のデジタルエンタテインメントのプラットフォームとも考えられる。ゲームそのものだけでなく、実況動画のキラーコンテンツであったり、Mod（改造データ。Modificationの略）を通じた改造コンテンツであったりと、単純なゲームの域に留まらない面があり、その将来性を高く評価したのではないか。

Minecraftの拡張性
- バニラのクライアントで追加機能GUIを作る
    - ![image](https://gyazo.com/44401bcbf823b2d103ef59b4d54824e9/thumb/1000)
        - これはSlimefunという大物の工業化プラグインのゲーム内ガイド
        - 実はチェスト(アイテムを収納する道具)のUIを使ったハックである
            - 本物のチェストはこう
                - ![image](https://gyazo.com/26d50a46a1f704e3ef3e96034b306ee7/thumb/1000)
        - ガイドの詳細画面
            - ![image](https://gyazo.com/d4661d7820e35c8566e0219ca1911008/thumb/1000)
            - 原子力発電所がどういう材料で作れて、どんな燃料を必要とするかが、チェストのUIとアイテムのホバーテキストで説明されている
    - 別の例
        - ![image](https://gyazo.com/f899286d33e604335e721a48d0dde903/thumb/1000)
        - これはEconomyShopGUIという、通貨とアイテムの売買を導入するプラグインだが、これもやはりチェストである
    - 各スロットに何を表示するか、どのスロットがクリックされたがをプラグインがフックしている
    - これはWebで昔行われてた「tableレイアウト」を彷彿とさせる
        - 柔軟なレイアウトをできる機能が当時のHTMLになかったので、表組みのためのtableタグを、罫線を全部消して表に見えないようにしてレイアウトに使うハック

- プラグインの開発
    - 0から作る方法はSpigotが丁寧に説明している
        - [https://www.spigotmc.org/wiki/spigot-plugin-development/](https://www.spigotmc.org/wiki/spigot-plugin-development/)
    - 西尾は0から作ったことはないが、既存のプラグインの改造は簡単だった
        - ソースコードをGithubからclone
        - Mavenをインストール
        - ソースコードを修正
        - ビルド
        - サーバのプラグインフォルダに置いてサーバを再起動
    - SlimefunのProgrammable Androidが
        - ![image](https://gyazo.com/13bbb1e3f3ead884f0b242b49ace8b6c/thumb/1000)
        - 指定した命令列を繰り返して実行するだけのものだったので
            - ![image](https://gyazo.com/421282cca9dbe33e2b6735d6bdb2c1b7/thumb/1000)
        - Pythonを実行できるようにしたw
            - ![image](https://gyazo.com/3c2874d8a7d6c3b3609124bdf9744f58/thumb/1000)

- プロトコル
    - 既に解析されている
    - 先程のチェストハックなら
        - チェストの各スロットがどういうIDか
            - ![image](https://gyazo.com/b196dbe84fb8b2c7b6b9c9f2cdc17261/thumb/1000)
            - [https://wiki.vg/Inventory](https://wiki.vg/Inventory)
        - スロットをクリックした時にどんなパケットが飛ぶのか
            - ![image](https://gyazo.com/522cdd83cae6491bf1264624f76543cc/thumb/1000)
            - [https://wiki.vg/Protocol](https://wiki.vg/Protocol)
        - が既知である

    - RCON
        - 管理者コマンド実行用プロトコル
        - 別プロセスからパケットを投げてゲーム内コマンドを実行できる
        - [https://wiki.vg/RCON](https://wiki.vg/RCON)
        - コマンドはバニラが提供しているものも、プラグインによって追加されたものもある
            - バニラのコマンドの例:
                - 指定座標の直方体に特定のブロックを配置
                - `/fill <x> <y> <z> <x> <y> <z> <block>`
                - [https://minecraft.fandom.com/wiki/Commands/fill](https://minecraft.fandom.com/wiki/Commands/fill)
                - Java版ではdestroyオプションでツルハシでの採掘相当のアイテム化が行われる
        - RCONパケットを投げる小さなプログラムが既にあるのでcronでパケット投げてサーバを制御するのも簡単

- ボットの開発
    - PrismarineJS/mineflayer
        - [GitHub - PrismarineJS/mineflayer: Create Minecraft bots with a powerful, stable, and high level JavaScript API.](https://github.com/PrismarineJS/mineflayer)
        - Node.jsでクライアントサイドを書ける
    - 西尾の作例
        - 成長した作物を収穫して新しく植えるボット
        - [https://scrapbox.io/files/61517e27f11b61001db4a93b.mp4](https://scrapbox.io/files/61517e27f11b61001db4a93b.mp4)
js

```javascript
function find_grown_nether_wart() {
  return bot.findBlock({
    point: bot.entity.position,
    maxDistance: SEARCH_RADIUS,
    matching: (block) => {
      return (
        block &&
        block.type === mcData.blocksByName.nether_wart.id &&
        block.metadata === 3
      );
    },
  });
}
```

js

```javascript
const toHarvest = find_grown_nether_wart();
if (toHarvest) {
  const { x, y, z } = toHarvest.position;
  const goal = new GoalNearXZ(x, z, 1);
  if (!goal.isEnd(bot.entity.position)) {
    log(`move to harvest: ${[x, y, z]}`);
    await bot.pathfinder.goto(goal);
  }
  log("harvest");
  await bot.dig(toHarvest);
  log("done");
}
```


- 建築物の書き出し
    - サーバファイルのフォーマットも既知なので読み出したり、プログラムで生成したりできる
    - バニラでも実はファイルへの読み書きが実装されてる
        - 「ストラクチャーブロック」を使う
        - ![image](https://gyazo.com/59dbb384903d640ec60abdf31a1992eb/thumb/1000)

- 西尾がまだ試してないこと
    - ワールドの一部をコピーして別のワールドにペーストできるはず
        - 追記 できた: [[World間Copy&Paste]]
    - Java版とBedrock版(Switchなどで動くバージョン)で同一サーバに繋げられるらしい
        - [https://github.com/GeyserMC/Geyser](https://github.com/GeyserMC/Geyser)
        - しかしSwitch版にはIPアドレスを指定して接続する機能がない
        - > On Minecraft Bedrock Edition, players on Xbox One, Nintendo Switch, and PS4 are limited to playing on 'Featured Servers' approved by Mojang/Microsoft.  [https://github.com/Pugmatt/BedrockConnect](https://github.com/Pugmatt/BedrockConnect)
        - BedrockConnectの解決方法
            - サーバ管理者がDNSサーバを立てる
            - Switchで遊ぶ人はネットワークの設定をいじってそのDNSサーバを使うようにする
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>それは…ちょっと誰にでも勧められる方法ではないな…
        - 追記: [[Minecraft Java版サーバにSwitchから繋ぐ]]
            - 繋ぐことはできたが遅い

物理オフィスのバーチャル化
- アフターコロナで出社しないことを前提として遠隔地へ引っ越した人がたくさんいる
    - 物理的なオフィスが社員のコラボレーションの場として使いにくくなった
- バーチャルな場を作ろうと考える人も多い
    - 関連サービスは無数にあるがいくつか例にあげて議論する
    - Oculus Room
        - 作り込まれたモデル
        - デバイスの特徴を活用した音声提示
        - しかしカスタマイズはアプリが提供している僅かなオプションだけ
            - ![image](https://gyazo.com/c6c59b2bb9b4b76005d010212ea96163/thumb/1000)
            - [src](https://www.youtube.com/watch?v=dYas7tyMfuM)
    - VRChat
        - ワールド、アバターともに圧倒的にカスタマイズ性が高い
        - しかしワールドを作ろうとすると？
            - 「まずUnityをインストールします」
            - 多くの人がここでドロップアウトする
        - アバターの自作は、アニメーションで関節が破綻しないようにするなどモデリングよりさらにハードルが高い
            - 多くの人はあるものから選ぶ
            - 「自分である」感がない
    - Minecraft
        - 大きめの箱の組み合わせで世界が構成されている
            - 人間が使うサイズの建物はブロックを積んで比較的簡単に作れる
            - 花を飾るなどのちょっとした手直しを誰でもできる
        - アバターも四角い箱の組み合わせ
            - 塗りも粗いピクセル
            - ブラウザ上で塗り絵して簡単に作れる
            - 例: [https://minecraft.novaskin.me/#](https://minecraft.novaskin.me/#)
                - ![image](https://gyazo.com/d8c85588b8c8f8c76242ecc596cfb9e9/thumb/1000)
                - 四角い箱に色を塗っただけには見えない複雑な形状に見える
                    - 実は各ボディパーツに一回り多いレイヤーがあって服や髪の毛にうまく使われている
            - 僕も作ってみた
                - 特にどうしたいというこだわりがないので普段着てそうな服を着てみたw
                - ![image](https://gyazo.com/d64736b2460b59fd7b4ee6359d497d09/thumb/1000)
                - これは基本的にレイヤーなしで、目の瞳だけレイヤーにしてピクセルっぽくない位置に置いている
- カスタマイズできないのは「自分たちのもの感」がない
- カスタマイズに外注が必要だと高コストだし、たとえ金銭的コストが解決しても要望を言語化することが負担
- これって「kintoneを使って社員がみずから業務システムを作る」というアプローチが好評なのと同じ構図
    - カスタマイズできない業務システムは不満があっても直せない
    - それを嫌って外注でシステムを作ると高コストだし、修正も高コストなので結局不満があっても直せない
- 現状のMinecraftで不足な点
    - 音声チャットがない
        - 一定距離に入った人だけとか同じ部屋の中の人だけとかの音声チャットが必要
        - 技術的にはプラグインからDiscordの音声チャンネルを制御することができるはずだが…
    - 全社員が集まるパーティをマイクラ上でやろう！
        - というアイデアが出てくることが容易に予想できるが、これは技術的チャレンジ
        - デフォルトでは同時接続20名までに制限されている
        - オプションで制限を緩めることは簡単だが、何人までサーバが耐えられるのかテストが容易ではない

IT部活応援
- 「やりたいこと」がすでに明確ならそれを支援してあげれば良い
- 「やりたいこと」が明確でない層
    - ゲームはインセンティブになる反面、ゲームを遊んだだけで終わってほしくない
- そこでマイクラ
    - 人間が単純作業を繰り返すより、自動化装置を組んだ方がいい
        - 実際プログラミング的思考のできるプレイヤーだらけの未踏ジュニアサーバでは…
        - ![image](https://gyazo.com/02a3a4236531d4ba9debf26461609371/thumb/1000)
        - ![image](https://gyazo.com/48ba56f96cfd31f0349c13027800f1d1/thumb/1000)

    - 人間が単純作業を繰り返すよりコマンドを覚えた方がいい
    - プラグインを入れて便利なツールやコマンド、新しいゲーム機能を追加
        - それをやるためには基本的にはSpigotやGithubの英語のドキュメントを読む必要がある
    - プラグインはオープンソース
        - ドキュメントを見てわからないことはソースコードを読む必要がある
        - もしくはGithubにissueを立てる
        - もしくはDiscordのチャンネルで英語で相談
    - プラグインの機能に不満なら実装をいじる必要がある
    - という感じでゲームからシームレスに現代的なプログラミング体験をするインセンティブが生み出される
- 中国ではゲル弾を射出する戦車ロボットで戦ったりしてる
    - ![image](https://gyazo.com/0144b1af634190716b3caf22ef34dffa/thumb/1000)
    - 手動コントロールを補うプログラムを書いて「プログラミングを学ぶと強くなって勝てる」というインセンティブの作り方をしている
        - Learn to winというキャッチフレーズ
            - ![image](https://gyazo.com/5170fa1ab74a3453ea083169c5c64836/thumb/1000)
        - 勝つために、画像認識などを学ぶインセンティブが生まれる
    - だがこのアプローチは、日本では兵器を連想させるものへのアレルギー反応が強いので採用しづらいのだろう
    - 平和なインセンティブが必要
- コスト
    - Minecraftのマルチプレイをする上ではサーバ費用がネック
    - Conoha VPSで大体こんな感じの費用感
        - ![image](https://gyazo.com/4f1d68559de5d04a260a1bca4027316f/thumb/1000)
        - 今回、よくわからないからとりあえず真ん中のやつを3ヶ月試してみてる
            - 年間4万は小中高生にとっては重い負担だろう
            - (なおテンプレートでインストールされて便利かと思ったが、これで入るのはバニラのサーバで、開始初日に止めて入れ直した)
    - 仮にこれをサイボウズが提供するなら？
        - 業務システムのインフラよりもSLA低めにして良さそう
    - 単に遊ぶだけにならないためには？
        - サイボウズの社員向けの部活支援と同じスキームで良いのではないか
        - つまり、資金援助をする代わりに共有の場での報告を求める
        - 技術情報を発信する側の立場を経験してほしい
        - 一方でパブリックなインターネットへの投稿に対してネガティブな感情を持ってる教師保護者は多い
        - たとえばkintoneをクローズドなSNS的に使うのはどうか

[[オンラインコラボレーション]]
