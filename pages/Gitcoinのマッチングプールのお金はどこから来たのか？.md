---
title: "Gitcoinのマッチングプールのお金はどこから来たのか？"
---

公式回答
- [Where does the Gitcoin Grants Matching Pool Money Come From? - 🧙 🧙‍♀️ Ideas and Open Discussion - Gitcoin Governance](https://gov.gitcoin.co/t/where-does-the-gitcoin-grants-matching-pool-money-come-from/9036)
    - 細かい話を割愛すると、最初の5回に関してはEthereum Foundationが出している
        - それからその実績を見てスポンサーが増えていった
    - 余談だけども[[Vitalik Buterin]]が当時の価値で約500万ドル相当の49兆[[Akita Inu]]トークン(AKITA)を寄付した話([src](https://www.gitcoin.co/blog/announcement-gitcoin-community-receives-generous-gift-from-vitalik-buterin))はユーモラスだな、「5億円分の秋田犬が寄付された」のか

[[Gitcoin]]の[[マッチングプール]]のお金はどこから来たのか？
> [0xtkgshn](https://twitter.com/0xtkgshn/status/1646386996540235777) ...[[Ethereum財団]]をはじめとする、[[Gnosis]]や[[ConsenSys]]などの大手クリプト企業です。なぜかというと自分たちが[[クリプトエコシステム]]で儲かっているので、[[エコシステム]]を支援するインセンティブがあります（しないと先細ります）
- > [0xtkgshn](https://twitter.com/0xtkgshn/status/1646387189012643840) ある程度まで大きくなると私営など問わずに公共に投資しなければいけなくなるのは、Bigtechの動きを見ても納得感あると思います。これは一つ、「ノブリスオブリージュは義務だ」という文脈と繋がります。
    - > [nishio](https://twitter.com/nishio/status/1646389824180588544) なるほど。[[利他]]とか[[ノブレスオブリージュ]]という解釈もできるけども、別の表現をすれば[[エコシステムへの投資]]が長期的にみれば良いリターンを生む[[長期投資]]である、ということだと理解しました
- [[Ethereumエコシステムは徴税できるので公共財へ投資できる]]
- [[OSS開発でお金を得ることができる世界線]]

$500kがスポンサーから提供されている
- これがマッチングプールの原資
- スポンサーからの分配には2.5%のキャップがある
    - キャップのある分配は数学的にはQuadratic Fundingではないからロバストネスを失ってるけど、細かいことは気にしてないようだ
- [Gitcoin Grants Round 15 kicks off Sept. 7](https://go.gitcoin.co/blog/grants-round-15-kicks-off/)
    - > The GR15 Main Round will distribute $500k in matching funds – with Quadratic Funding, that $500k can go a looong way in helping fund and sustain the web3 projects of tomorrow.
    - >  The Main Round is our longest-standing Grants Round. The Main Round is designed to support early-stage open-source software projects in web3. Our main round matching sponsors are: Yearn, Polygon, ENS, Figment, Chainlink, Starkware, Wicklow Capital, and 1inch!
    - >  The main round is unique because there is a 2.5% matching cap of the total main round pool – once a grant has hit  $12.5K in matching funds from the GR15 main pool, they’re no longer eligible for additional matching. This matching cap makes sure that less popular grants receive matching funds!
個別の寄付が3万人いる
- 1065プロジェクトに総額$832kを寄付した
- この寄付自体は直接各プロジェクトに行って、寄付行為を投票とみなしたQuadratic Fundingでマッチングプールから分配したのかな？
- [Gitcoin Grants Round 15: Round Results & Recap](https://go.gitcoin.co/blog/gr15-results#main)
    - > We had 31,148 donors contributing to our Main Round, giving over $ 832k to 1,065 projects. WOW!
    - >  Funds will be allocated based on the QF mechanism with a maximum cap in place in order to ensure matching funds are evenly distributed across a breadth of grants. For GR15, matching funds were capped at $12,500 per grant.


2023-05-13
> [@0xtkgshn](https://twitter.com/0xtkgshn/status/1657306202194452480?s=20): .@nishio
> 「Gitcoinのマッチングプールのお金はどこから来たのか？」に対するいい回答あった
- > [VitalikButerin](https://twitter.com/VitalikButerin/status/1242896875524689920) Those who say "grant funding by whales is a bad mechanism, we need better thing X" are missing the point.
- >  Gitcoin grants is a *trial run* for quadratic funding. The long-run goal is to have tx fees from L2/apps (eg. rollup MEV auctions) feeding into the matching pool directly.
    - > [VitalikButerin](https://twitter.com/VitalikButerin/status/1242897980388257792) Remember the primary dictum of good economic design: tax the congestible (aka scarce resources aka -ve externalities), subsidize the public goods.
    - >  Congestible: tx inclusion, MEV, short names, attention, status symbols...
    - >  Public goods: network security, dev, research, education..
- (DeepL) Gitcoin grantsは、二次的な資金調達のための*試運転*です。長期的な目標は、L2/アプリ（ロールアップMEVオークションなど）からのTX手数料が直接マッチングプールに供給されるようにすることです。混雑するもの（[[希少資源]]、[[逆外部性]]）には課税し、[[公共財]]には補助金を出すという、優れた経済デザインの基本を思い出してください。
    - [[混雑するものに課税し公共財に補助する]]
[/tkgshn/QFのMatching Poolに企業が寄付するよりも良い方法](https://scrapbox.io/tkgshn/QFのMatching Poolに企業が寄付するよりも良い方法)
- > [@nishio](https://twitter.com/nishio/status/1657360476999917568): @0xtkgshn 「人気のものから税金を取って公共財に投資する」という国家の重要な機能の一つをEthereumが担うというわけだね
- > 長期的なビジョンと「今はそれをtrial runしてるだけ」というのが明言されててとてもよい
    - [[人気のものに課税し公共財に投資する]]

[[MEV]]: [MEV Auction: Auctioning transaction ordering rights as a solution to Miner Extractable Value - Economics - Ethereum Research](https://ethresear.ch/t/mev-auction-auctioning-transaction-ordering-rights-as-a-solution-to-miner-extractable-value/6788)

