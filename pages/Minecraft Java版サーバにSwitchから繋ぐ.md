
MinecraftのJava版互換サーバ(Spigot, Paperなど。この記事で使ってるのはPaper)に
Nintendo Switch(つまりBedrock版)から
### IPアドレス指定で
接続する方法

解決が必要な問題点
- SwitchにはIPアドレスを指定して接続するUIがない

解決方法
- 特集サーバへの接続時に行われるドメイン名解決を、
- この目的のためのDNSサーバで行わせることで、
- 本来のサーバではなく「ワールド選択用サーバ」(BedrockConnect)に接続させる

サーバ管理者側がすること
- GeyserとFloodgateの導入
    - これはBedrock版で参加できるようにするために必要
クライアント側がやること
- SwitchのDNSの設定を変更する
    - [解説動画](https://www.youtube.com/watch?app=desktop&v=zalT_oR1nPM)
    - DNSの接続先は 104.238.130.180でよい
        - これは下記リストのBedrockConnectサーバの一つ
            - [Publicly available BedrockConnect instances](https://github.com/Pugmatt/BedrockConnect#publicly-available-bedrockconnect-instances)
- 特集サーバへ接続する
    - ![image](https://gyazo.com/1a31de1139167725abdf73f9205c54cb/thumb/1000)
    - 接続先はなんでも良い
    - MSアカウントでログインしていないともしこのワールド一覧が出ないようだ
- 「ワールド選択UIを実装したワールド」につながる
    - ![image](https://gyazo.com/0e0f2f932317037fbfcb93dee5e21c4c/thumb/1000)
- 接続したいサーバのIPアドレスを入力して接続する
    - ![image](https://gyazo.com/605932dfe098a4bcab696f1f03fda435/thumb/1000)
- 目的のJava版サーバにSwitchから接続できた
    - ![image](https://gyazo.com/2a07e89f65088fe383fed96a002515f4/thumb/1000)
    - 見栄えはJava版とは少し異なる(額縁の透明化が機能してなさそう)

2022-07-16
- 前回試した時は遅くて使い物にならない印象だったが「問題なくプレイできたよ？」的な意見があったので再度検証した
- 前回はサーバを自分で立てたが、面倒なので今回は公開サーバを使うことにした

2022-01-19
- ログインするまではJava版よりもだいぶ長くて20秒ぐらいかかるが、フレームレートは完璧、という意見もあり、ワールド依存っぽい

まとめ(2021-10-27)
- 接続はできた
- 現実的にプレイできる速度ではなかった(5FPSくらい)
- 改善する方法はわからない

![image](https://gyazo.com/8374c001060f835727f5aff6ccc4043a/thumb/1000)
- サーバリソースパックが適用されていない、どうすれば適用されるかわからない

やり方
- EC2にBIND9を入れてDNSサーバ(A)を立て、特定のドメインを自分のJava版のサーバ(B)に向ける
    - [Setting up on Linux · Pugmatt/BedrockConnect Wiki](https://github.com/Pugmatt/BedrockConnect/wiki/Setting-up-on-Linux)
- Switchのネットワーク設定でDNSサーバを指定できるので(A)にする
    - [解説動画](https://www.youtube.com/watch?app=desktop&v=zalT_oR1nPM)
- Bedrock版はUDPで19132番ポートに繋ぎにくることに注意
    - 最初TCPと間違えてファイヤーウォールで阻まれてた
- サーバ選択画面が必要なければBedrockConnectサーバを起動する必要はない
    - デフォルトの設定なら19132番ポートが使われるはずなので(B)とぶつかるはず、起動しないことにしたので深追いしてない
- サーバ(B)にはBedrockのパケットを受け取れるようにするプラグインが入っている
    - [https://github.com/GeyserMC/Geyser](https://github.com/GeyserMC/Geyser)
    - [https://github.com/GeyserMC/Floodgate/wiki](https://github.com/GeyserMC/Floodgate/wiki)

---ログ
> [nishio](https://twitter.com/nishio/status/1453246991853621259): DNSぜんぜんわからん(Minecraftをしています(？))

> [nishio](https://twitter.com/nishio/status/1453248083354136584): マイクラの走ってるEC2にBIND9を入れて、セキュリティルールでDNSのポートを開け、自宅のルータのプライマリーDNSをEC2のアドレスにしたんだけどちゃんとできてるか確認しようとしてMacBookでdigしたらサーバは127.0.0.1だとか言われて頭を抱えてる

> [nishio](https://twitter.com/nishio/status/1453248966611644420): ネットワークの基礎知識が足りなすぎて何を確認して問題を切り分けたらいいのかすらわからない…

> [kaorun](https://twitter.com/kaorun/status/1453253521344761856): もしかして: AnyConnectとか入ってる会社のマシン

> [nishio](https://twitter.com/nishio/status/1453254117237968903): あああ…なるほど…

> [kaorun](https://twitter.com/kaorun/status/1453254477415387139): Macだとちと違うかもしれませんが、AnyConnect入ってるマシンだと、DNSがAnyConnect側にもってかれてローカルネットワークのDNSは参照してくれないみたいで、DNSなんもわからん状態に(いろんな意味で)。

> [nishio](https://twitter.com/nishio/status/1453256949051674632): 管理下にないマシンで試したら127.0.0.1になりませんでした！

> [nishio](https://twitter.com/nishio/status/1453258106977275909): うーむ、そもそもルータの設定でDHCPサーバ機能がオフだった…Switchは一体どこからDNSの情報を得ているのか…？？？

> [nishio](https://twitter.com/nishio/status/1453258225218899972): Switchの上でipconfigとかしたい()

> [nishio](https://twitter.com/nishio/status/1453258650437537794): なるほど、そもそもルータの設定をいじる必要はなかった？！
> m.youtube.com/watch?v=zalT_o…

> [nishio](https://twitter.com/nishio/status/1453262905756078085): サーバへの接続で失敗するようになったのでDNSで接続先をすり替えることには成功したっぽい。次はなぜ失敗するのかについて…動画を見ると一旦ワールドに接続した形でダイアログ出してるように見えるな

> [nishio](https://twitter.com/nishio/status/1453265751440347143): うーんわからない、一旦離れるか

> [nishio](https://twitter.com/nishio/status/1453291426519867403): 今見返して、さっき気づきかけたことにようやく気づいたのだけど「サーバ選択画面を出すサーバ」と「接続したいサーバ」の両方が同一マシン上でBedrockのポートをlistenできるわけがなく、「Already used」的なエラーが出てないのは、どちらかがエラーを握りつぶしてて気づけないだけなのでは。

> [nishio](https://twitter.com/nishio/status/1453292205792243720): 時系列としては「接続したいサーバX」が先に起動してるのでこれがポートを掴み、「サーバ選択画面を出すサーバY」がlistenに失敗してるけど例外を握りつぶしてるのでは。Yを終了するのは試したが、Xを起動せずにYを立ち上げるのは試してない。これを検証すべき。

> [nishio](https://twitter.com/nishio/status/1453302861937393681): >BDSは、TCPを使用するJava Editionとは違い、UDPを使用する。
> AAAAAAHHHH
> minecraft.fandom.com/ja/wiki/Bedroc…

> [nishio](https://twitter.com/nishio/status/1453304155234254848): ワールド選択サーバには接続できた！！ pic.twitter.com/kp5x6Y6Nbb

> [nishio](https://twitter.com/nishio/status/1453304776674926593): うむう pic.twitter.com/UlMQhjl0LM

> [nishio](https://twitter.com/nishio/status/1453305501157105666): お、1.17.40対応のバージョンがリリースされてる、入れ替えるだけか

> [nishio](https://twitter.com/nishio/status/1453308334560346112): できた！(サーバリソースパックは適用されてないが…) pic.twitter.com/4gis0PD9ok

> [nishio](https://twitter.com/nishio/status/1453312156678586375): そして残念ながら深刻な低FPS。5くらいかな。

> [nishio](https://twitter.com/nishio/status/1453314577790234626): サーバのロードアベレージとかには余裕があるので、Switchの性能か、パケット変換の遅延のせい、ちょっと簡単には解決できなさそうだなぁ