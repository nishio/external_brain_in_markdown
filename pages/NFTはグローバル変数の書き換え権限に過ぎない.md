---
title: "NFTはグローバル変数の書き換え権限に過ぎない"
---


<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>この続きの文章として「このグローバル変数を割り当てて自分が書き換え権限を持つことを『NFTの所有』と表現して、価値を過大評価させる詐欺が行われることになった」と書こうとしている。ファクトチェック

<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
要旨：趣旨は近いが、表現は少し調整した方が正確です。
- Ethereum は「世界規模の共有状態（global/singleton state）」を全ノードで合意し、EVM がその状態遷移を決定する“世界コンピュータ”。この比喩は妥当です。 ([ethereum.org](https://ethereum.org/en/developers/docs/intro-to-ethereum/?utm_source=chatgpt.com), [Alchemy](https://www.alchemy.com/docs/what-is-ethereum?utm_source=chatgpt.com))
- NFT は ERC-721 で「tokenId → 所有者アドレス」等のエントリとして記録され、所有者または承認済みオペレータだけが transfer を起こせる、という“権限”設計になっています（＝任意に書き換えるのではなく、コントラクトのロジック経由で状態が更新される）。 ([Ethereum Improvement Proposals](https://eips.ethereum.org/EIPS/eip-721?utm_source=chatgpt.com), [OpenZeppelin Docs](https://docs.openzeppelin.com/contracts/4.x/api/token/ERC721?utm_source=chatgpt.com))
- なお メタデータは発行側が更新できる設計も多い（ERC-4906など）。「所有者＝あらゆる書き換え権」ではありません。 ([Ethereum Improvement Proposals](https://eips.ethereum.org/EIPS/eip-4906?utm_source=chatgpt.com))
- 市場面では ウォッシュトレード等の価格つり上げが広く確認されています。最新の暗号犯罪レポートでも NFT を含む市場操作が整理されています。 ([Chainalysis](https://www.chainalysis.com/blog/crypto-market-manipulation-wash-trading-pump-and-dump-2025/?utm_source=chatgpt.com))
- ラグプル等の詐欺で有罪・起訴に至った事例（Mutant Ape Planet ほか）も複数あります。 ([司法省](https://www.justice.gov/usao-edny/pr/nonfungible-token-nft-developer-pleads-guilty-international-scheme-defraud-nft?utm_source=chatgpt.com))
- さらに、NFT の購入＝著作権などの法的権利の取得ではないのに、そこを誤解させる説明が価値の過大評価につながるケースも指摘されています（マーケット規約・法学文献）。 ([OpenSea](https://opensea.io/tos?utm_source=chatgpt.com), [Oxford Academic](https://academic.oup.com/ijlit/article/doi/10.1093/ijlit/eaae018/7746479?utm_source=chatgpt.com))

推奨の書き方（例）
「この『世界規模の共有状態』では、NFT は tokenId→所有者 というエントリで表現され、所有者（または承認者）が移転を承認できる。一方で、権利内容を実体以上に誤解させる説明やウォッシュトレード等の操作により価値を過大に見せかける詐欺が相次いだ。」 ([Ethereum Improvement Proposals](https://eips.ethereum.org/EIPS/eip-721?utm_source=chatgpt.com), [Chainalysis](https://www.chainalysis.com/blog/crypto-market-manipulation-wash-trading-pump-and-dump-2025/?utm_source=chatgpt.com), [OpenSea](https://opensea.io/tos?utm_source=chatgpt.com))
ポイント：
- 「書き換え権限」は「移転を承認できる権限」程度に言い換えると正確。
- 「詐欺」は**具体的な手口（ウォッシュトレード／ラグプル／権利誤導）**に分けて示すと、過度な一般化を避けつつ事実に基づきます。 ([Chainalysis](https://www.chainalysis.com/blog/crypto-market-manipulation-wash-trading-pump-and-dump-2025/?utm_source=chatgpt.com), [司法省](https://www.justice.gov/usao-edny/pr/nonfungible-token-nft-developer-pleads-guilty-international-scheme-defraud-nft?utm_source=chatgpt.com), [OpenSea](https://opensea.io/tos?utm_source=chatgpt.com))
このトーンなら、技術的にも法的にも踏み外さずに批判点を明確化できます。

