
2021-09-19 この1週間で色々学んだのでメモしておく
![image](https://gyazo.com/acb5b341ffb730c790161d7825c67558/thumb/1000)

2021-09-10
- 未踏ジュニアのゲームチャンネルでAmongUsをやる日程調整の投稿に冗談でマイクラ絵文字をつけたら9人も押した
    - マイクラサーバ需要あるなーとなった

2021-09-11
- Bedrock Edition(BE)をRealm(公式が提供するオンラインサーバ)で遊んだ経験しかなくて、Java Edition(JE)だと色々MODを入れられるみたいで面白そうだなぁとは思っていた
- 何をしたい？と聞いてもあんまり明確な意見はなかった

2021-09-12
- 朝5時に「考えてても特に方針見えてこないのでまずは手軽な方法でえいやっとやってしまうか」と意思決定
    - (時間帯のせいだw)
- [Conohaのマイクラテンプレート](https://www.conoha.jp/vps/media/mine-semi/multi-server/)を使う
    - やると決めて17分後にはもうサーバ立ってた、楽ちん
    - Paperが良いという話を聞いたがよくわからない
        - 後から理解したこと:
            - 公式が提供しているサーバと、それをリバースエンジニアリングしてパッチを当てたものが存在している
                - その発想はなかった、歴史が長くてプレイヤーが多いとそんなことも起こるのだな
            - PaperMCやSpigotがキーワード
- そこからJEのクライアントをダウンロードしてサーバに繋ぐまで30分掛かった
    - たいまつの作り方がわからない
        - JEには「レシピを知らないので一覧に表示されない」という状態がある？
    - シードやゲームルールを指定する画面を経由しないでいきなり始まってしまった
        - JEにはそういう画面はないので変えたいなら設定ファイルをいじるか管理者がコマンドを使う
        - BEではゲーム内でGUIで変えられるのでなんでコマンドがあるのかなと思ってたが、なるほど設定ファイルを書き換えて再起動するよりはゲーム内コマンドで変える方が楽だわな
- えっJEってBEよりモンスター固くない？
    - 暗い平地にスポーンしたためゾンビに取り囲まれて死亡
    - 僕が悪戦苦闘しながら土壁の拠点を作ってたら、40分ゲーム内2日でネザーゲートが開いてた、文明の差を感じるw
- 一通りマルチプレイしてからSpigotとかPaperとかを調べ、今のサーバを止めてPaperのサーバを立ち上げるべきだと判断した
    - [Getting Started — PaperDocs 1.17.1 documentation](https://paper.readthedocs.io/en/latest/server/getting-started.html)
    - デフォルトのサーバやセーブデータなどは/opt/minecraft_serverにあった
    - ここでpaperを走らせた
    - vanillaのセーブデータは自動で変換された
    - ターミナルからコマンドを受け付けるのでscreenで動かすのが一般的らしい
    - systemdはよくわからないので保留
- ユーザ管理よく知らない
    - `$ adduser nishio`
    - `$ usermod -aG sudo nishio`
    - `.ssh/authorized_keys`
    - とりあえず公開鍵認証でログインできるようになった
- プラグインを入れられるようになった
    - ワールドの中のものをレンダリングしたい
        - [Overviewer](http://docs.overviewer.org/en/latest/)を入れたがセーブデータのフォーマットが変わったせいかうまく動かない
        - [dynmap](https://www.spigotmc.org/resources/dynmap.274/)を入れた
            - クォータービューで見たかったがデフォルトでは真上からの地図で混乱した
            - クォータービューは画面の右端にわかりにくいメニューがいた
                - ![image](https://gyazo.com/96fb6c4cfa1a48131b83d8fb6d1e43d9/thumb/1000)
            - 離れたところの人がやってる建築のプロセスが見れて面白い
- スポーンチャンクの保護を外さないと他のプレイヤーがブロックを壊せない
    - `server.properties`: `spawn-protection=0`
- screenからデタッチしないままsshが固まって、アタッチできない
    - `screen -dr`
- 新しいプレイヤーが来て農場を作り始めた
    - ![image](https://gyazo.com/29be4f43b59ff3a9c6680e0fd1939eff/thumb/1000)
- 色々プラグイン入れた
    - [holographic-displays](https://dev.bukkit.org/projects/holographic-displays) 光るホログラムの文字が出せるようになって見づらい看板の代わりに
    - [EconomyShopGUI](https://dev.bukkit.org/projects/economyshopgui): ショップ機能が入った、しかしユーザ間取引かと思って入れたんだがそうではなさそう
    - [worldedit](https://dev.bukkit.org/projects/worldedit)、まったくedit目的に使いこなしてないけどjumptoで見てるブロックの上に飛ぶので便利
- サーバがkilled
    - 4GBメモリのVPSで`java -Xmx4G`はおかしい
    - `java -Xmx3G`にしたらその後発生してない
- ![image](https://gyazo.com/3752b8f89b05e2878af5620fac2edfbe/thumb/1000)
    - 半自動回収までできた、村人が何故か増えてくれない、増えたら閉じ込めて働かせるつもりなのに
- 装飾的建築が好きな人が拠点をアップデートしてくれた
    - ![image](https://gyazo.com/631a684c307653affdba724673159fab/thumb/1000)


2021-09-13
- dynmapの更新頻度を下げる
- [Slimefun](https://github.com/Slimefun/Slimefun4)を知った、入れた、発電機などが追加される工業化プラグインです。
    - 新規ユーザでない場合はガイドを持ってないみたい
        - `/sf guide` でゲットできる
    - 頑張って粘土を掘ってレンガを作ったのに解釈間違いだった、Multiblockは複数のブロックをレシピの通りに「ワールドに配置する」ことで機能する装置
    - 技術ツリーをアンロックするのに経験値が必要、死んで失ったばかりだから僕何もできないw
        - JEではサボテンをかまどで焼いた時の経験値が金鉱石と同じ
            - あちこちの砂にサボテンを植えた
            - 経験値かまどバグがJEで再現するのか検証→再現しなかった
- screenにアタッチして管理コマンドを入れて終了/再起動するのめんどくさい
    - シグナルとかでコントロールできないのか？
    - SIGINTでできる [How to stop PaperMC when not in console · Issue #1757 · PaperMC/Paper · GitHub](https://github.com/PaperMC/Paper/issues/1757)
:

```
$ ps -a | grep java
$ sudo kill <PROCESS_ID>
```

- 拠点にエンチャントテーブルできてた！ 牛と羊もいっぱい
- BEでつかってた溺死式ニワトリ自動屠殺装置、JEだと動かない
    - アイテムが浮いてホッパーに吸われない  see [[マイクラのニワトリ]]
- マイクラにはパケットを送ってコマンドを実行する機能[RCON](https://wiki.vg/RCON)がある
    - クライアント実装: [https://github.com/Tiiffi/mcrcon](https://github.com/Tiiffi/mcrcon)
- javaの起動をbashのwhileで包むことで自動的に再起動できる [src](https://raw.githubusercontent.com/Zachoz/CrashPrevention/master/start.sh)
- 設定ファイルをGithub管理にした
    - RCONもオンにした `server.properties` の `enable-rcon=true` `rcon.password=XXX`
- ![image](https://scrapbox.io/files/613edb268b15b5001d7dc906.png)

2021-09-14
- 拠点の隣にSlimefunの研究施設を建ててくれた
    - 装置は嵩張るしどんどん増えるので拡張できる形にして正解
    - 最初木造だったが火を使うため火災が発生した
- 苗木自動回収植林場を作ってくれた
    - ![image](https://gyazo.com/673abd87cf0c4da5cdb9b21f4b8493d4/thumb/1000)
    - 取ったら植える。白樺とオークならOK
- ![image](https://scrapbox.io/files/613fb818832489001d5044f2.png)

2021-09-15
- [[マイクラのサボテン]]
    - サボテン自動収穫農場をラボの上に作るか農場に作るか
        - →水をラボの上で使って事故った場合にレッドストーン回路が全滅するのがヤバいから農場でやることにした
    - スタック可能
        - 一階以外はホッパーを使わなくても単に穴から落とすだけで下のホッパーに入る
- 経験値トラップを作ってくれた
- 首都でサボテン量産→かまどで焼くと大量に緑の染料ができるから村人に売りつけてエメラルドにできると都合が良い
- ![image](https://gyazo.com/4b18b963081a93239605b93b5e740e34/thumb/1000)
- [Lockette](https://dev.bukkit.org/projects/lockette) でチェストが置けなくなる: `illegal chest removed`
    - ラージチェストがらみ [src](https://github.com/Acru/Lockette/blob/ac6ad1ef6d8ca5848f49135a18679cf9d0773136/src/org/yi/acru/bukkit/Lockette/LocketteBlockListener.java#L386)
    - 原因究明コスト払わずアンインストールで対処
- Horse moved wrongly問題
:

```
[01:16:18 WARN]: Horse (vehicle of XXX) moved wrongly! 0.2619578421472575
[01:17:18 WARN]: XXX was kicked for floating too long!
[01:17:18 INFO]: XXX lost connection: Flying is not enabled on this server
```

    - 普通に馬に乗ってて速すぎるってログが出るのも不思議だがその1秒後に空を飛んでる判定でkickされてるの、これ馬で走ってただけなのでは感がある
    - changed spigot option: [Server spaming moved wrongly/tooquickly | SpigotMC - High Performance Minecraft](https://www.spigotmc.org/threads/server-spaming-moved-wrongly-tooquickly.237103/)
    - rebootついでにパイプと自動クラフトが入りました
- [[Transport-Pipes]]すごく良い
    - ホッパーやドロッパーをレッドストーンでオンオフして無理やり実現してる自動仕分けが、うるさくもなく重たくもならずにコンパクトに収まりそう。
    - パイプのマテリアルは起動した時にダウンロードするか聞かれた、入れないとこうなる？
        - ![image](https://gyazo.com/16f6c2cb4f567fa6aa0c87c3cd680f4f/thumb/1000)
- ニワトリ屠殺装置「育ったら横のボタンで水を出して、20秒ほど待つとみんな溺死するので、水を抜いてアイテム回収」という感じになった
    - BEだとハーフブロックの上に水を置きっぱなしで育ったやつから溺死してちょうどよかったんだけど、JEだとジタバタ泳いで水の中で死ぬせいでアイテムが水の上に浮かんでしまいホッパーで吸えない
- Slimefun
    - 爆発ツルハシ(Explosive Pickaxe)研究したが素材が足りなくて作れない
- 自動バックアップ機能してない問題
    - `[07:40:51 INFO]: [DriveBackupV2] No backup method is enabled`
    - > DriveBackupV2 is a plugin that aims to provide an extra layer of security to your data by backing it up remotely.
    - Dropboxに保存することにした
        - 何らかの理由によってサーバが消滅しても1時間以内のセーブデータがあるからリカバリできる
- Twitter
    - > [nishio](https://twitter.com/nishio/status/1438069685338083332): 今時のMacユーザがリモートのLinuxマシンにファイルを送ったり取ってきたりするのには何を使うのがオススメですか？
        - > (ターミナルでscpコマンドを打ちながら「これは古臭いやり方なのでは？」と思っている)
    - > [nishio](https://twitter.com/nishio/status/1438371395839295488): この件、ユースケースを説明しなかったので多種多様な意見が集まりましたが、マイクラサーバにプラグインのjarを置く話で、VSCodeのRemote Explorerで開いたら見慣れた表示で追加できたし、設定ファイルの編集も楽、元々やってたgitでの設定管理とも一元化されて万々歳という結論になりました
- Java option: [Tuning the JVM – G1GC Garbage Collector Flags for Minecraft](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/)

2021-09-16
- 「別に急いでないんだけど適当なタイミングでサーバを再起動したい」的な時にどうやってタイミングを決めたらいいか
    - →定期的自動再起動というアイデアをもらった
    - 平日16時に自動再起動、土日は緊急メンテ以外では再起動なし
        - 「設定の更新があった時だけ再起動」にしたいけど、それは後々
- RCON経由で終了再起動はできたが、むしろ上記のstart.shの問題は「再起動を止める方法が、人間がJavaプロセス終了から5秒以内に再度SIGINTするしかない」というところ…
    - そんなものターミナル観察してないと無理じゃん
    - bashでの条件分岐を調べる
:

```
$ [ -f "autorestart" ]; echo $?
1
$ touch autorestart
$ [ -f "autorestart" ]; echo $?
0
```

    - `disable_restart`ファイルが存在するなら再起動しないようにした
bash

```
if [ -f "disable_restart" ]; then
    break
fi
```

    - cronの書き方を調べる…
cron_settings

```
30 15 * * 1-5	/usr/local/bin/mcrcon -p <PASS> "say The server will reboot in 30 minutes!"
55 15 * * 1-5	/usr/local/bin/mcrcon -p <PASS> "say The server will reboot in 5 minutes!"
0  16 * * 1-5	/usr/local/bin/mcrcon -p <PASS> "stop"
```

        - 平日16時に30分前と5分前の予告付きで再起動するようになった
- [[Transport-Pipes]]でかまどにサボテンや燃料を入れられる
    - 本来のホッパーのメイン業務である「ワールドのアイテムを吸い取る」はホッパーにしかできない
    - ホッパーを無理矢理使ってパイプライン的なことをやってたのが、素直なパイプに変わる感じ
- 再起動の完了をMattermostに通知とかできたらいいんだけどな。
    - Discordならあった [discord-webhook](https://www.spigotmc.org/resources/discord-webhook.84489/)
    - [DiscordSRV](https://www.spigotmc.org/resources/discordsrv.18494/)にした
        - 各ユーザの login / logout /death と サーバの stop / start が通知される
        - Discordとマイクラのそれぞれのチャットが中継されるはずなのだけどされない、原因不明
        - → 2021-09-19 LunaChatと同時に使うとぶつかるからDiscordSRVの設定でLunaChatのフックをdisableする必要があるという記述があった！
- ニワトリ屠殺のために20分たって育ってから20秒だけ水を出したい
    - それ日照センサーでできるのでは、と教えてもらった
        - マイクラの1日は20分
        - 晴天時の最高信号強度の時だけ水を出すとアイテムデスポーンより短い時間
    - レッドストーン回路でパルスエッジ検出回路をどうやって作るのか
        - オブザーバーで見るだけで立ち上がり立ち下がりが取れると教えてもらった
    - これでニワトリの自動屠殺はできた

2021-09-17
- Slimefun スポナーを回収できるピッケルがあるので見つけたものを拠点に移設できる
- [Eternal Light](https://www.spigotmc.org/resources/eternal-light.50961/)　モンスターがスポーンする暗さの時に警告表示
    - ネザーは辛いから普通の間隔で松明を置いてもわきつぶしにならない
- Slimefun: Industrial Miner、とりあえず燃料に石炭を1個入れて、8ore分動くだけのはずなのにずっと動いてるなと思ったら自力で石炭を取って採掘を続けてたっぽい、98個も手に入った
    - 同じところで2回動かして2回目は何も得られなかったので7×7で岩盤まで掘ってるっぽい
    - すごい！石炭ガッポリ！と思うが、他のツールの作成で必要な合成ダイヤモンドを作るのに石炭4スタック消費するのでinもoutも増えてる…
- ![image](https://scrapbox.io/files/6144cbbfdfb9c0001d3fd878.png)

2021-09-18
- Slimefun、連続してる木材をまとめて取れる斧を研究した
    - 複雑な形状の木をきれいに取れるから便利
    - 拠点周りの鬱蒼とした森を間引いてラージチェスト1杯の木材の山ができた
- [[Transport-Pipes]]、クラフトパイプの挙動を理解した
    - 自動仕分け機に入れた、銅鉄金、石炭、レッドストーン、ラピスラズリが自動的にブロックに圧縮されてから格納されるようになりました
- Slimefun 爆発ツルハシ、3マスまとめて掘れるので地下を見通しの良い感じに掘るのに便利、しかし耐久があっという間に減る、作るの大変だったのに…修繕装置ができるまで保留か
    - 斧は長持ち
- Slimefun 金鉱石をすりおろさないで良いように石から作るパイプラインを作っときました
- 溶岩増殖機の側に植林して「これで木炭作り放題だ〜」とかやってたら溶岩から葉っぱに引火して大火事に！
    - ラボが防火建物でよかった…
    - 蓋をしたら大丈夫かなぁ
        - →ダメでした、下の大釜から火の粉がでてるのかな
    - 事故った時の被害を抑えようと川辺に置いてるけどむしろ防火の屋内におくべきか
- Basic Circuit Boardの研究をして作り方を見て「えっ…」となってる
- 放置アカウントでやってほしい連打作業とかって何があります？→丸石製造機
    - 丸石装置を調べて作った [ref](https://zenzenzenchan.com/minecraft-cobblestone-auto-farm/)
    - 連打ではなく長押しか
        - PyAutoGUI
            - > [nishio](https://twitter.com/nishio/status/1439283282626039809): PyAutoGUIなるものが面白そうなのでゲーミングPCにPythonをインストールしている。WindowsでのPython環境構築は何年振りなのか。
            - > [nishio](https://twitter.com/nishio/status/1439283698919100417): Ctrl+dして「あれー、終了できないぞ」という
            - pipで入る
python

```
import pyautogui
import time
time.sleep(5)
pyautogui.mouseDown()
```

            - 簡単
    - ツルハシを供給
        - 放置するとツルハシは割とすぐ壊れる
            - 石のツルハシは3分ちょいで壊れる、鉄でも2倍ない、ダイヤなら10倍以上ある
        - 自動クラフトが可能なのだから定期的に作って投げつければ良いのでは
- ![image](https://scrapbox.io/files/614636760e598200232f6e01.png)

[[マイクラJE日記week2]]