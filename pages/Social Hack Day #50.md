---
title: "Social Hack Day #50"
---

2023-05-27 [[MintRally UX Upgrade Sprint]]の第一歩として参加した
- [[官民共創HUB]]

> [@codeforjapan](https://twitter.com/codeforjapan/status/1662362592822837248): 記念すべき50回目となった今日の #socialhackday では、６つのプロジェクト、オンライン＋オフライン合わせて30+名の皆さんにご参加いただきました🙌 17時から進捗報告＆プチ懇親会です💃
> ![image](https://pbs.twimg.com/media/FxHlh_raYAAorMS.jpg)

> [@hal_sk](https://twitter.com/hal_sk/status/1662287811620519936?s=20): ソーシャルハックデー50回目、開催中です。
> 今日はハイブリッド開催で、会場参加もたくさん！ありがとうございます🙌
> 今日はgussuri(睡眠記録)、Open Data Package manager、流山Make our City、HackDays(web3)、もりポ(脱炭素)、アフターピル検索のプロジェクトが登録されてます。
> #socialhackday
> ![image](https://pbs.twimg.com/media/FxGh87cacAAKHrZ.jpg)

> [@nishio](https://twitter.com/nishio/status/1662378408721154049?s=20): Social Hack Day `#50` に参加したよ！
>  [https://opensea.io/ja/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/442](https://opensea.io/ja/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/442)
- ![image](https://gyazo.com/d68b0457b8780640055fe9f667805995/thumb/1000)

[[MintRally]]は上記のような「参加証明NFT」を発行するサービス
- 発行した「証明書」がNFTなのでMintRallyのサービスの中に閉じていない
- 実際、上記のTweetではMintRallyで発行したNFTを、世界最大規模のNFT取引プラットフォーム[[OpenSea]]の上で表示している
- > [@nishio](https://twitter.com/nishio/status/1662311155069779968): Plurality Tokyoに参加した証明のNFTがOpenSea上で見れる／見せれるのを教えてもらった！デフォルトでhiddenになってるだけで、unhideすればいいだけだった！
- >  [https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375](https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375)
    - ![image](https://gyazo.com/1b36ba74e71bddb2a280725fc0fcddf7/thumb/1000)

全体
- 物理会場に来ていてもまずZoomに入る
    - チャットがURLの共有に大活躍
- Code for Japan
    - [[行政の共創]]
        - [[行政への依存]]ではなく
- オンラインオンリーとハイブリッドとを隔月でやってる
- [[g0v]]の[[jonthon]]からインスパイア
- 自己紹介
    - Notionを情報共有の場として使う
    - Notionのアクセス権をもらってテーブルに自分のレコードを追加
        - > Code for Japanでは、SlackとNotionを活用してコミュニティ運営をしています。 Code for Japanのこれら2つのワークプレイスには、シビックテックに興味がある方なら、どなたでもご参加いただくことが可能です。
            - [コミュニティ | 活動 | Code for Japan](https://www.code4japan.org/activity/community)
        - 僕は初めてだったのでその場でSlackとNotionに参加した
    - 今回のイベントページを見つけようとして、検索と間違えてHomeのタイトルを編集してしまったw
        - すぐ戻したからセーフw
        - 今回はZoomのチャットのURLからいった
        - 検索欄が目立つところにないのでサイドバーのツリー表示からたどるのが想定フローなのだろう
            - 「最近更新されたページ」を見る方法はあるのかな？
        - [Social Hack Day #50](https://www.notion.so/code4japan-community/Social-Hack-Day-50-84fd842a943c4ab4800011298cc41f55)
            - 自己紹介は3つのキーワードを書く
            - 時間が限られてる時に自己紹介をするのに良い仕組み
            - 周りの人がどんなことを書いているか、自分が書いてる最中にも見える
            - 3つキーワードがあると長々と話すことが防げるし、「西尾です、よろしくお願いします」みたいな情報ゼロの自己紹介をする人が連鎖してそういう空気になり自己紹介の場自体の有用性をスポイルしてしまうリスクも避けられる
            - このタイミングで初めての人にリアルタイム共同編集の体験をさせるのはうまいオンボーディング設計だな
                - Scrapboxを使う場合でも参考にできそう
- 各プロジェクトの紹介と今日やることの発表
    - 全部それぞれ面白そうだね
    - 現状がどうで、今日は何をする予定かを話す
    - ある種の「[[朝会]]」のような感じ

各プロジェクトチームに分かれる
MintRally

(時間軸のログではなく、後から調べたこと考えたことも加筆して再構成した)

最近Ethereumのアドレスがない人でも受け取れるようになった？
- MAGICLINKを使う？
    - [https://magic.link](https://magic.link)
- [[non-custodial]]？custodial？
    - MAGIC側がEthereumのアドレスを持って、それに対してメールアドレスでのアクセスを提供するものだと理解した

ネットワークの切り替えとは何か
- Ethereumのメインネット
    - これは高い
- Polygonという別のネットがある
    - これはEthereumに安く書き込める
    - なぜ？
        - トランザクションをバッチにして書き込むから
        - なるほど、コンピュータにおいてメモリフェッチのコストが高いからより高速なキャッシュメモリを間に挟む的なやつね
        - バッチで書き込むならバッファの分だけ実際にEthereumに書き込まれるまでの遅延が増えると思うがどの程度増えるのか？
    - こういうのをL2プロトコルという？
        - PolygonのハッシュがEthereumに書き込まれる？

秘密鍵どうしてる？
- パスワードマネージャーにいれてる
- 大金が入ってるなら推奨は印刷して金庫に入れること
- 結局リスクと利便性のトレードオフ
    - 大金が入ってないならリスクが小さいから雑にしてもいい
- ウォレットという呼び名がユースケースによってはミスマッチだよね
    - というわけでこのページではもっぱら「アドレス」と読んでます<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

発行されたNFTがMetaMask上で見えない
- ちゃんともらえたのかな？となる
- これは単にMetaMaskのUIの設計の問題
    - MetaMask側がアドレスに新しいNFTが付与されてるかをチェックして表示してないだけ
    - 表示したいなら新しいのがあるよと教えてやる必要がある
        - インポート
- ![image](https://gyazo.com/e4bf9b8250f21290e8b10b738c40c481/thumb/1000)![image](https://gyazo.com/9889a634940ed50de7c2d9c7d9c62dd9/thumb/1000)
- コントラクトのアドレスとIDで特定できる
- MintRallyのURLを教えたりする必要はない、これが面白いところ
    - つまり、よくあるスタンプ発行サービス的なやつはスタンプの情報がそのサービスの中にしかないから、他のサービスに情報を共有しようとするとURLとかで伝えるしかない
    - 一方でMintRallyが発行したNFTはブロックチェーンという「共有メモリ」に書き込まれているので、どこに書き込んであるかのアドレスを渡すだけでよい
    - 受け取る側がMintRallyのことを知る必要はない

OpenSeaにもインポートできる？
- OpenSeaはインポートするまでもなく自動的に入る
- [https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375](https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375)
    - ![image](https://gyazo.com/4428eba06a17f1d4d18f37b4a8b19a1b/thumb/1000)
    - あった！
- 非表示になってるだけ
    - ![image](https://gyazo.com/5f16c77b6166955ca184313d58383540/thumb/1000)
- unhideすると表示される
    - 日本語UIだと「再表示」になってる
- > [@nishio](https://twitter.com/nishio/status/1662311155069779968): Plurality Tokyoに参加した証明のNFTがOpenSea上で見れる／見せれるのを教えてもらった！デフォルトでhiddenになってるだけで、unhideすればいいだけだった！
- >  [https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375](https://opensea.io/assets/matic/0x7d895ca96caa5344ec0b732c6e1defa560671e14/375)
    - ![image](https://gyazo.com/1b36ba74e71bddb2a280725fc0fcddf7/thumb/1000)
    - OpenSeaがTwitterバッジなども出してくれてる
- OpenSeaでも詳細が見れる
    - ![image](https://gyazo.com/25a60f338bbec888e713461845676305/thumb/1000)
    - このコントラクトアドレスをクリックすると詳細がでる

[[Polygonscan]]
- 具体的な生データを見る方法はあるのか？
- Polygonscan
- [https://polygonscan.com/address/0x7d895ca96caa5344ec0b732c6e1defa560671e14](https://polygonscan.com/address/0x7d895ca96caa5344ec0b732c6e1defa560671e14)
- ![image](https://gyazo.com/68257d2cd089618c173de2dd79cc494b/thumb/1000)
    - そのコントラクトに対するトランザクションが見える
- ![image](https://gyazo.com/ae8a82b7eb3880607586c02a5d1b0b2e/thumb/1000)
    - コントラクトのコードも見える
        - てっきりバイトコードにコンパイルした状態かと思ったが[[Solidity]]の元コードがみれるのか
        - これはMintRally側がPolygonscanに提出してる？
        - [[公明正大]]アピールのために？
- バイトコードの表示とデコンパイルボタンがあった
    - つまりソースコードが提出されてない場合はバイトコードだけ共有されるので、読みたい人はデコンパイルする必要があるという理解
    - ![image](https://gyazo.com/e9caf664bcde022769488f4e68f0adca/thumb/1000)
- [https://polygonscan.com/token/0x7d895ca96caa5344ec0b732c6e1defa560671e14?a=442](https://polygonscan.com/token/0x7d895ca96caa5344ec0b732c6e1defa560671e14?a=442)
    - id=442のトークン
    - これが僕のもらったNFT
    - ![image](https://gyazo.com/92e99d66c049ac08ed2dd6e5372a1d3c/thumb/1000)
    - 最初にもらったからFromがnull

Etherscan
- Ethereum
- [僕が売ったNFT](https://opensea.io/ja/assets/ethereum/0x495f947276749ce646f68ac8c248420045cb7b5e/96364121663629944399678349944126304514402904357872840150623063082905167200257)の[トランザクション](https://etherscan.io/tx/0x3470a91e915879cfb9d0a0f02d7e24f657b5861f43e31d4305e3d4228cb3338b)
- ![image](https://gyazo.com/13b57ea13ed15edc41cd0bda17b8db20/thumb/1000)
- おっ、これ売買した二人の財布の中身の金額変動が見えてるのではw
    - 台帳が全世界公開共有されてるって仕組みを考えれば当たり前だが、ウォレットを財布とイメージしてたらギャップあるよな
    - 確かにここに100万円とか入れてたら、手に札束を持って歩いてるようなものか
        - ひったくりされそう

これらを[[Block Explorer]]と呼ぶ

Q: 実際に発行する側をやる場合、どれくらい掛かるのか？
- 参加者が無料で受け取る方法と、参加者がGAS代を払う方法がある
    - GAS代=コンピューティングリソースの代金
    - [[受益者]](=この場合NFTを受け取る人)が払うのが一般的
    - しかしイベント参加者に参加証を配るというサービスの目的にはミスマッチ
        - 受け手がウォレットにMATICを持っている必要があるから
- MintRallyは両方できる
    - 参加者が増えるにつれて費用も増える
    - 大雑把に一人当たりどれくらい？
        - 5〜10円くらい

Testnetで発行者を試してみよう
- PolygonのTestnetをMumbaiと言う
- Testnet、てっきりローカルで自分で動かすものかと思ってたがそうではないらしい
- 何が違い？
- 通貨に金銭的価値がない
    - その場合、テストネット上でのトランザクション実行のガス代が誰からも支払われないことになるが…
    - メインネットのGAS代に含まれてるんだろうな、ある種のフリーミアム
    - だとするとテストネットで行えることが、メインネットより制限されてないといけないわけだがそれは何か？

参加証明NFTを何に使うか？
- NFTにどのような[[効用]]([[Utility]])を持たせるかは設計次第
    - この質問回答、非エンジニアにニュアンスが伝わらないかも
    - 「へー、磁石は鉄にくっつくんですね！これは何に使うんですか？」「何に使うかはあなたの自由ですけど…」みたいなノリ
- [[POAP]]は事例集を公開してる
    - [https://poap.directory/](https://poap.directory/)
    - 例えば特定のトークンを持っている人だけ参加できるZoomリンク
        - [[トークンゲート]]
    - [[Proof of Humanity]]
        - [[SoulBound Token]]
            - これは譲渡不可なトークンを作るアプローチだが[[Vitalik]]は「ブロックチェーン上にすべての移転記録が残ってるのだから新しい仕組みを作る必要はない」と言っていたらしい
                - ブロックチェーンをdigればよい
                    - →[[Block Explorer]]
            - プロトコルのレイヤーではなくアプリケーションのレイヤーでよい
            - 最初の所有者を表示するか、最終の所有者を表示するか、ビューの違いに過ぎない
    - POAPは進化しない、参加回数によって進化する機能がMintRallyの優れてる点
        - これによって「何度も訪れている常連さんにサービス」的なことが可能になる

Testnetでイベントを作る
- つまずいたところをMiroに貼る
- MATICのガス代がなぜ1000000と表示されるのか？
- TestnetのMATICに通貨価値がないならその取得手段が購入とは別に存在するのでは？
    - ある。Polygon Faucet

Dune
- Dashboardを作れるサービス

開発する
- [https://github.com/hackdays-io/mint-rally](https://github.com/hackdays-io/mint-rally)

[[Hardhat]]
- 手元でブロックチェーンを動かす
- 今回はSolidityの開発はしないので入れなくてよい

MintRallyは自前でデータを持ってない
- チェーンだけでやってる
- 自前でデータを持たずにこんなウェブアプリが作れるってすごいな

Callback
- 別ページを見せておいて終わったら通知
- (一般名詞すぎて検索で見つけられなかった)

[[Pinata]]
- IPFS
- たぶんメディアデータはここにいく

とりあえず簡単にできそうなところとしてイベントグループを逆順にしてみる
- forkしてpushしてpullreq(普通の流れ)
    - [https://github.com/hackdays-io/mint-rally/pull/250](https://github.com/hackdays-io/mint-rally/pull/250)
- 事前に手元でテストケースを走らせるとかはない
- issueはタイトルは英語、中身は日本語のこともある

[[DeWork]]
- Trelloみたいなもの
- 何が違うのだろう

[[HACKトークン]]
- MetaMaskにまずHACKトークンの情報を教えないといけない
- ![image](https://gyazo.com/70dc4e21f0e983a84a4c16e19992503f/thumb/1000)
- できた！
- [[貢献トークンは感謝の可視化]]

中頃にシャッフルタイム(他のプロジェクトを見に行く)があったが、ヘッドセットを持ってきていなくて目の前の人とZoomの向こうの人の会話を聞くことが困難だった(スピーカーから出すとこちらの人の声が二重になる、スピーカーを止めると向こうの人の話し始めを聞き損ねる)

最後にプロジェクトの進捗シェアと、良かったことシェア
- プルリクを送るところまでできてよかった
