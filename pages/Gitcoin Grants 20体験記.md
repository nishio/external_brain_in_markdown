---
title: "Gitcoin Grants 20体験記"
---

from [[日記2024-05-03]]

前々から[[Gitcoin]]での[[Quadratic Funding]]を体験してみたいと思ってたらちょうど[[Gitcoin Grants]] 20が行われてる旨の呼びかけを目にしたので体験してみる

> [0xtkgshn](https://twitter.com/0xtkgshn/status/1785971222582579699/photo/1) 現在15番目ぐらいです！Arbitrumでクリプトを持ってる人は協力していただけると！！！あと5日です
>  ![image](https://pbs.twimg.com/media/GMkLOavakAADz2E?format=jpg&name=medium#.png)
- [[Arbitrum]]初耳
    - でもないな[[Arbitrum Orbit]]って単語をメモしてた

> [digdaox](https://twitter.com/digdaox/status/1782951323165700169) Gitcoin Grants 20開始
>  デジタル公共財を支援するための環境作りを促進させるために、Gitcoinの寄付ラウンドに参加しています。
>  現在、QFを活用した公共財への資金提供のためのツール開発をしているので、ぜひご支援ください！
>  寄付はこちら（寄付期間：4/23〜5/7）
![image](https://gyazo.com/758df89b00525d681b8b1e9bdf0b2f6e/thumb/1000)
とりあえずカートに入れてみる

![image](https://gyazo.com/bde6da6495fd4efd7c0af8a2f6c6bdbc/thumb/1000)
ふーむ？
カートに入れてからそれにいくら払うか決めるのか
1[[ARB]]っていくらなんだろ

![image](https://gyazo.com/85cbd7309a81c3c15c82d268171bc2b3/thumb/1000)
1ARBは1ドルくらい
僕が1ドル寄付すると[[マッチングファンド]]から21ドル程度出る計算

![image](https://gyazo.com/6eafda78c8062b0c92fd3f57d02f8892/thumb/1000)![image](https://gyazo.com/cfef0d2cf332a3769556c5cd73f9f474/thumb/1000)
16倍払えば4倍の84ドルになって、100倍払えば10倍の210ドルになる、これは[[Quadratic Funding]]の仕組み

ウォレットを接続してみる
![image](https://gyazo.com/2f5a638130a60e200dd0dd281d747557/thumb/1000)![image](https://gyazo.com/a175ddf3a5804d770bc67d99ae9ed0d5/thumb/1000)
まあ、ARBは持ってないからそうなるわな
そもそもネットワークはこれでいいの？よくなさそう
![image](https://gyazo.com/2f1339494963a63b76c192427f232f2e/thumb/1000)

> [nishio](https://twitter.com/nishio/status/1786267423362203843) カートに入れるところまではできたけどArbitrumをどこからどこにどうすればいいかよくわからない！(どこかの[[DEX]]でETHか何かと交換してから何らかの方法でArbitrumチェーンに入れる？)
> [yudai007004](https://twitter.com/yudai007004/status/1786276008414572745) 僕はですが、[Arbiturmのブリッジ](https://bridge.arbitrum.io/?destinationChain=arbitrum-one&sourceChain=ethereum)を利用して、ETHをEthereum(or その他)→ Arbiturmに移動させて、DEX(例えばUniswap)を利用してswap(ETH→ ARB)したら出来ました！
> [nishio](https://twitter.com/nishio/status/1786407646989582413) 情報ありがとう！やってみます！

ブリッジとは何か...
とりあえずアクセス
- [https://bridge.arbitrum.io/?destinationChain=arbitrum-one&sourceChain=ethereum](https://bridge.arbitrum.io/?destinationChain=arbitrum-one&sourceChain=ethereum)
- MetaMaskと接続
- ![image](https://gyazo.com/8e0ca1fb4d68c792c5a1ed1bd1809db5/thumb/1000)
- えーと1ETHっていくらだ
- ![image](https://gyazo.com/62e1fe6e2bde9a028079fb69136196ea/thumb/1000)
- ということはウォレットに5万円くらい入ってるのか
- じゃあ「Suicaに5000円チャージしよう」のノリで5000円くらい移動してみるか
- ![image](https://gyazo.com/8ee19107f0ec3641395fad0dce98683a/thumb/1000)
- ![image](https://gyazo.com/aefd30fd5b22f6e1cf184ec1ab5d8946/thumb/1000)
- 手数料が$3.65、銀行振込ばりに掛かるw
- ![image](https://gyazo.com/dc00ba2eb762125c0165da06d7b383dd/thumb/1000)
- 15分待てとのこと

待ってる間に
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[Arbitrum]], [[Arbitrum One]], [[Arbitrum Orbit]], [[ブリッジ]]とは何ですか？検索して日本語で説明して
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Arbitrum、Arbitrum One、Arbitrum Orbit、そしてブリッジについての解説です。
- Arbitrum は、イーサリアムのスケーリングソリューションで、レイヤー2のオプティミスティックロールアップ技術を使用しています。これにより、イーサリアムと同等のセキュリティを維持しつつ、取引コストを大幅に削減します​ (Bridge to Arbitrum)​。
    - [Quickstart: Arbitrum bridge | Arbitrum Docs](https://docs.arbitrum.io/arbitrum-bridge/quickstart)
- Arbitrum One はArbitrumの主要なネットワークで、オプティミスティックロールアッププロトコルを採用しており、イーサリアムのメインネット（レイヤー1）に直接バッチ処理される取引を支えています​ (Arbitrum Docs)​。
    - [A gentle introduction: Orbit chains | Arbitrum Docs](https://docs.arbitrum.io/launch-orbit-chain/orbit-gentle-introduction)
- Arbitrum Orbit は、開発者が独自のカスタムチェーンを許可なしに作成できるようにするためのフレームワークです。これにより、プロジェクト固有のニーズに合わせた高度なカスタマイズが可能となり、新しいアプリケーションやプロトコルイノベーションのための「チェーンの宇宙」を提供します。Orbitチェーンは、Arbitrum OneやArbitrum Novaなどの既存のArbitrumレイヤー2チェーン上に展開することができます​ (Arbitrum)​​ (Arbitrum Foundation)​。
    - [Arbitrum Orbit](https://arbitrum.io/orbit)
    - [Arbitrum Orbit — Launch new chains in the Arbitrum ecosystem](https://arbitrum.foundation/orbit)
- ブリッジ は、イーサリアムなどの親チェーンとArbitrum Oneや他の子チェーン間での資産の移動を容易にするためのツールです。このブリッジを使用して、ユーザーはETHやERC-20トークンを親チェーンから子チェーンへ、またはその逆に移動できます​ (Bridge to Arbitrum)​。

これらの技術を使用することで、Arbitrumは高いカスタマイズ性とスケーラビリティを持つ分散型アプリケーション（dApp）の開発を強力にサポートします。また、Orbitを利用することで、プロジェクトは自身のアプリケーション専用のチェーンを持つことができ、更なるパフォーマンスとガバナンスのコントロールを実現できます。

15分待てと書いてあったが15分掛からずにsettleした
![image](https://gyazo.com/ad04832fe402f105da6291d7b2eb9475/thumb/1000)

で、これでEthereum(Network)からArbitrum One(Network)にETH(Token)が移動できたから、次はETH(Token on Arbitrum One)をARB(Token on Arbitrum One)と交換する必要があるわけね

[[Uniswap]]にMetaMaskを接続
![image](https://gyazo.com/557e4f811e0de3d7f278d406647e8320/thumb/1000)
わかるぞ、ここだろ(初見殺しのUIにだいぶ苦労させられたのでわかるようになったw)
![image](https://gyazo.com/a6a6e36939ffced4a17300de21a0ef44/thumb/1000)
Arbitrumに切り替える
![image](https://gyazo.com/c817776d27ab9143f143dfd0de2769a2/thumb/1000)
![image](https://gyazo.com/7d0455e898c57d47b00f8ee3934e0c3c/thumb/1000)
えっ、わからん

![image](https://gyazo.com/90ab296f2590754d8f705f962693f068/thumb/1000)
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>Arbitrum Oneを使用する際にMetaMaskでカスタムネットワーク情報を検証することは重要です。MetaMaskにカスタムネットワークを追加するときは、特に以下の情報を慎重に確認してください：
- ネットワーク名（Network Name）：MetaMaskがネットワークを識別するために使用する名前です。
- ネットワークURL（Network URL）：MetaMaskがネットワークにアクセスするために使用するURLです。
- チェーンID（Chain ID）：MetaMaskがネットワークのために取引を署名する際に使用するチェーンのIDです。
- 通貨記号（Currency Symbol）：ネットワークのネイティブ通貨のためにMetaMaskが使用する通貨記号です。
- ブロックエクスプローラーのURL（Block Explorer URL）（オプション）：MetaMaskがあなたのアカウントや取引を調査するために誘導するURLです。

不正確な情報が表示された場合、または何かが間違っているとMetaMaskから警告があった場合、正しい情報を確認するために次のステップを踏むことが推奨されます：
- Chainlistを訪問する：提供されたチェーンIDやネットワーク名で検索し、一致しない情報を特定します。
- ネットワークの名前をGoogleで検索する：公式ウェブサイト、Twitterやその他のソーシャルメディアの存在、フォロワーの数や評判、ネットワークに関するニュース記事などを通じて、ネットワークの合法性を評価します。

これらの情報源から、ネットワークが合法的で信頼できるかどうか、そして提供された情報が正確かどうかを判断することができます。不確かな場合は、そのネットワークの追加を拒否し、さらに調査を行い、後で再試行することが賢明です。

[[Chainlist]]初耳
[https://chainlist.org/?search=42161](https://chainlist.org/?search=42161)
![image](https://gyazo.com/f776cd0691577bf5af38b9b70ac4127d/thumb/1000)
もしかしてArbitrumからArbitrum Oneに名前が変わったってこと？

公式ドキュメントを見る
- [RPC endpoints and providers | Arbitrum Docs](https://docs.arbitrum.io/build-decentralized-apps/reference/node-providers)
- ![image](https://gyazo.com/7c56166b87fe49d124f2751fd20fe16e/thumb/1000)
比べる
- ![image](https://gyazo.com/90ab296f2590754d8f705f962693f068/thumb/1000)
名前以外は一致してるからいいか
許可する
![image](https://gyazo.com/6ae200eb73c6c4a2403cb4b01356008f/thumb/1000)

で、何だっけ
そうそうUniswapね
![image](https://gyazo.com/0f6da2e796af76f70169795b69e9c1a5/thumb/1000)
Balance: 0.01になってる、正しい
全部ARBにしよう
![image](https://gyazo.com/2bcde683028480dcf6b187e5df7bdb71/thumb/1000)![image](https://gyazo.com/baf3d0211d38c0065b280091288a3cec/thumb/1000)
おっと、手数料分が足りない
![image](https://gyazo.com/a98651ac01cabf7d8bebacf45e51a1ac/thumb/1000)

こうかな
![image](https://gyazo.com/b8689e98000790e1e99abcaa8fd4f0bc/thumb/1000)
できた
![image](https://gyazo.com/6516b9006f10b918b54a0e446b8fc845/thumb/1000)
[Arbitrum Transaction Hash (Txhash) Details | Arbiscan](https://arbiscan.io/tx/0x67d46c7a17623a4b47f03baecfcadc488dab664e59b98a8efceab4a1ff0b50b2)

えーと、それでなんだっけな
[[Gitcoin+DigDAO]]
- [Gitcoin | Explorer](https://explorer.gitcoin.co/?utm_source=grants.gitcoin.co&utm_medium=internal_link&utm_campaign=gg19&utm_content=program-rounds#/round/42161/25/156)
[[Gitcoin+DeSci Tokyo]]
- [Gitcoin | Explorer](https://explorer.gitcoin.co/#/round/42161/39/19)

とりあえず予定通り[[Dig DAO]]に16ARBいれてみる
![image](https://gyazo.com/d05286d3d92a008517bd116b2c577e03/thumb/1000)
MetaMaskをConnectする
![image](https://gyazo.com/9fc632883910badb269a66eb5d689a99/thumb/1000)
Submitできそう！
![image](https://gyazo.com/a40c0e65319cd87a6ab47391548f76a6/thumb/1000)
![image](https://gyazo.com/72cb470f89f2b68d0098b1f9521b5f60/thumb/1000)
![image](https://gyazo.com/b80e6f88e45ee7fac544336dd6a35f14/thumb/1000)
![image](https://gyazo.com/a390a3f1cf6de66e5d4d5a2136036694/thumb/1000)
できた！
Share on Xを押すとこうなる
![image](https://gyazo.com/75c004525628ea0307c6ad6e00e79d9b/thumb/1000)
[https://explorer.gitcoin.co/#/contributors/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610](https://explorer.gitcoin.co/#/contributors/0xd50c28f7Cda33859DFD34Bbab518cD50AcD5d610)
![image](https://gyazo.com/4dd9ae8a2febe7af5b19676c7edc1cec/thumb/1000)
ほー、こうなるのね

残りを[[DeSci Tokyo]]に入れる
のこりのARBがいくらかはどこで見るのか...？
![image](https://gyazo.com/f759a840bd2eac6e16d816e21f12ecac/thumb/1000)
足りないってわかるならいくら残ってるかわかるだろ、表示してよw
11.8かな
![image](https://gyazo.com/0085fea4aed63a159d8e0a220d35e6eb/thumb/1000)
あー、整数なんだ、じゃあ11だな、100円分くらい残っちゃうけど仕方ない
![image](https://gyazo.com/f634ac800ca911869fc9e45f36058c66/thumb/1000)
できた
![image](https://gyazo.com/53b1aab8ea9b77cb6925743c23b73b68/thumb/1000)

ちょっと予想外だったところ
![image](https://gyazo.com/709a4c35f5b41b4aee8695048a35264d/thumb/1000)![image](https://gyazo.com/f634ac800ca911869fc9e45f36058c66/thumb/1000)
DigDAOに$16いれて+$83なら、DeSci Tokyoに$11入れたらもっと少ないEstimated matchだと思ったのに予期せず$322もついた
謎だなと思ったけどDonation Historyをみたら
![image](https://gyazo.com/5ed3268373991fb1670ffda14230fa48/thumb/1000)
こうラウンドが分かれてたので、マッチングプールも分かれてるんだろうな
DeSciのマッチングプールが大きいのか、dApps & Appsと比べて競争相手が少ないのか
どこで調べるんだろう

ここか(Top page)
![image](https://gyazo.com/dcd3508990c35464aba73cf6b3280402/thumb/1000)
比較
![image](https://gyazo.com/8ee881c14369390c9d221ce9f7121b6d/thumb/1000)![image](https://gyazo.com/4dee1052efa909466ebb571eab69ef9f/thumb/1000)
DeSciのマッチングプールは大きくはないが、プロジェクトも少ない

統計情報
dApps
![image](https://gyazo.com/08e55def491bce4e2ae457ee1d26e523/thumb/1000)
DeSci
![image](https://gyazo.com/684a1ed465a5b262e246b8743a5676e9/thumb/1000)

![image](https://gyazo.com/0df786061bd4bc364861564e4f3faadf/thumb/1000)
- [https://reportcards.gitcoin.co/42161/25](https://reportcards.gitcoin.co/42161/25)
![image](https://gyazo.com/d329e3537bd21bc54ae7cfb1a5977685/thumb/1000)
- [https://reportcards.gitcoin.co/42161/39](https://reportcards.gitcoin.co/42161/39)




計算
dApps
![image](https://gyazo.com/08e55def491bce4e2ae457ee1d26e523/thumb/1000)
DeSci
![image](https://gyazo.com/684a1ed465a5b262e246b8743a5676e9/thumb/1000)
dApps: Total Crowdfunded 130K USDが36k Donationsなので1つあたり3.6USD
DeSci: Total Crowdfunded 5467 USDが470 Donationsなので1つあたり11.6USD
分布の形状が同じだとするなら
sqrt(3.6) * 36000 == 68305.197459637
sqrt(11.6) * 470 == 1600.7623183970816
の比を取って、同じ額をdonationしてもDeSciの方が影響力が43倍高い
一方マッチングプールはDeSciの方が12倍小さいので
結果同じ額をdonationした時にマッチングプールから得られるお金はDeSciが3.6倍大きい

![image](https://gyazo.com/709a4c35f5b41b4aee8695048a35264d/thumb/1000)![image](https://gyazo.com/f634ac800ca911869fc9e45f36058c66/thumb/1000)
実際には16ARB(4^2)で4 * 21、11ARB(3.3^2)で3.3 * 97だったので
97 / 21 で、だいたい4.6倍
ま〜、オーダーとしてはあってるだろう、たぶんDeSciの方が参加者の人数が少ないので分布の偏りが大きくて、その方がsqrt取った後のvoteの和が小さくなるから、同じ金額のdonationで得られるvoteの全体に占める割合が大きくてなるのだろう

談合が問題視されるのもよくわかる
僕が1500円くらい使って、寄付された人が5万円弱を手に入れてるわけなんだけど、じゃあ「1万円キックバックするからこの手続きをやって」って言ったらどうなるか、やる人いるのでは
正直こんなにマッチングファンドがつくとは思ってなかった
100円入れて2000円もらえる、1600円入れて8000円もらえる、10000円入れて20000円もらえる、という比率だと2000円を山分けするのはしょっぱいし、1万円使って2万円得て山分けだと作業をしないで1万円を持ち逃げするインセンティブが生まれちゃうわけで、あんまり上手くボロ儲けの構図を作ることができないんだよね
これはマッチングファンドに対する参加者が少なすぎて、寄付に対するマッチングが大きくなりすぎてる時に発生する問題なのかな

# 2024-05-08
> [yudai007004](https://twitter.com/yudai007004/status/1787681522352538009) 残り21時間くらいです！
>  現在20人の方がコントリビュートしてくれています！
>  DIDやSSI、分散型PDSに興味がある方はぜひ目を通してみてください！

> [yudai007004](https://twitter.com/yudai007004/status/1787682192174535067) Monasについては下記からご参照ください！
> Monasは分散型Personal Data Storeです。データの相互運用性とデータの主権を同時に実現することを目的としています。
> 詳細はこちら: [https://docs.google.com/document/d/1stQUrYfhbEcIilbOaRzCUfETRXiCWzo-E60MJ0CvnQg/edit?usp=sharing](https://docs.google.com/document/d/1stQUrYfhbEcIilbOaRzCUfETRXiCWzo-E60MJ0CvnQg/edit?usp=sharing)
> 今回はプロトタイプの実装として、読み込みアクセス制御と状態管理に焦点を当てて実装しました！実際にCryptreeのアルゴリズムの実装とブロックチェーン上で状態管理をするための実装を行いました。その中で鍵の管理の問題や鍵の導出アルゴリズムをどう実装するかなど課題を見つけられました。
>  こちらのドキュメントにプロトタイプの詳細が書いてあります！
>  [Filecoin-Data-Economy-Hackathon/docs/prototype.md at document · Monas-project/Filecoin-Data-Economy-Hackathon](https://github.com/Monas-project/Filecoin-Data-Economy-Hackathon/blob/document/docs/prototype.md)

> [yudai007004](https://twitter.com/yudai007004/status/1787682234725761295) 日本語もあります！docs.google.com
>  Monas: Privacy, Data Interoperability, and Self-Sovereignty in Decentralized Personal Data Store v1...
>  Monas: 分散型パーソナルデータストアv1におけるプライバシー、データの相互運用性、自己主権...
>  ![image](https://pbs.twimg.com/card_img/1786960983539531776/CVyLFRWl?format=jpg&name=small#.png)

![image](https://gyazo.com/29b6d025295d5d7b0867ba71709e7772/thumb/1000)![image](https://gyazo.com/40ea1f3874a8dd78d810976e7fab4297/thumb/1000)
![image](https://gyazo.com/60705277c2e4b7e6c7aed0f438f2aaed/thumb/1000)![image](https://gyazo.com/824766909dbc463f0198af7b20e26262/thumb/1000)
[https://arbiscan.io/tx/0xc04273ea7e08ac29c9231c99d3cb2ed50a552f096954269f085bead2959b4358](https://arbiscan.io/tx/0xc04273ea7e08ac29c9231c99d3cb2ed50a552f096954269f085bead2959b4358)
![image](https://gyazo.com/bb5f2844fc7a38b9c693d374723e85fd/thumb/1000)
![image](https://gyazo.com/5d7180ed66330aa6061d80fe42a6e34a/thumb/1000)

> [nishio](https://twitter.com/nishio/status/1787870355622895828) ARBのことを教えてもらったのにプロジェクトに気付いてなくて寄付し損なってたので、情報料として雑誌1冊分くらい寄付しておきました(プロジェクトのことはよくわかってないから情報の対価として)

これは15ARBで$111なのでDeSciとdAppの間くらいの係数だね

# 2024-05-12
> [0xLide](https://twitter.com/0xLide/status/1789443220222705966/photo/1) FF外からすみません。
>  GG20はETHとUSDCとARBをうけつけていたのでUniswapの工程は必要がありませんでした...ただcryptoを普段から触ってないと扱いづらいのは同意します。体験記色々と学びになりました
>  ![image](https://pbs.twimg.com/media/GNVgLTbbsAAgx1p?format=jpg&name=medium#.png)

> [nishio](https://twitter.com/nishio/status/1789459124599791883) 情報ありがとうございます！加筆しておきます！

