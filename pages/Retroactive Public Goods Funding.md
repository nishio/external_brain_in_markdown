---
title: "Retroactive Public Goods Funding"
---

- 2021年7月20日 [Retroactive Public Goods Funding. Note: The Optimism team has long been… | by Optimism | Optimism PBC Blog | Medium](https://medium.com/ethereum-optimism/retroactive-public-goods-funding-33c9b7d00f0c)
    - Optimism公式Mediumが「Retroactive Public Goods Funding」を掲載し、[[Vitalik Buterin]]がその中で「How the retroactive public goods funding DAO works」でメカニズムを詳述。ここが公的な初出とされる。
- 2021年9月10日
    - Vitalik Buterin と [[Karl Floersch]] がポッドキャストで「年初から温めていたアイデア」としてRPGFを議論。
        - [Vitalik Buterin & Karl Floersch: Retroactive Public Goods Funding](https://www.intothebytecode.com/1-vitalik-buterin-karl-floersch-retroactive-public-goods-funding/)



<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
[[Vitalik Buterin]]は「Retroactive Public Goods Funding（RPGF）」を 「先に価値を生み、あとで評価して報いる」新しい公共財ファンディング手法として提唱しています。要点は「将来の有用性を予測するより、既に役立った成果を振り返って合意形成する方が簡単」という洞察です。この仕組みは Optimism Collective などで実装され、実際に数十億円規模の資金が配分されています。

1. 着想と基本原理
- 1-1. 「事後」の方が合意しやすい
    - 従来の助成は「これから役立つはず」という計画ベースで審査するため、情報の非対称性や過大評価のリスクが大きい。
    - RPGF は成果が出た後に審査・報酬するため、実際のインパクトを指標にでき、合意が取りやすい

1-2. 仕組みの最小構成
- 資金プール: 財団・プロトコル利益・寄付などを積み立て。
- 成果提出: 開発者・研究者などが「過去の貢献」を申告。
- インパクト評価: バッジホルダー（審査員）が投票や QF 等で重み付け評価。
- トークン／現金配分: 重み比例で報酬を配分。
Vitalik はこれを「十分な資金を持つオラクル（判定機関）を設置するだけで公共財市場を形成できる」と説明しています。
- [Vitalik Buterin & Karl Floersch: Retroactive Public Goods Funding](https://www.intothebytecode.com/1-vitalik-buterin-karl-floersch-retroactive-public-goods-funding/?utm_source=chatgpt.com)

Vitalik は「QF と RPGF をレイヤー化し、まず QF で種まきし、成果が出たものに RPGF で大きく報いる」ハイブリッドを推奨しています」

5. 現在の論点と課題
- 評価のスケーラビリティ: Round 3 で 500+ 件を審査したが、工数が急増。
- インパクトの定量化: オープンソース貢献・教育・基盤研究など成果形態が多様で、一律評価は困難。
    - 一律の評価基準で評価できないものを評価する仕組みが必要なんだよ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
        - [[和で評価するとジェネラリストが選ばれる]]
- 人気投票化リスク: 巨額配分になると知名度が高いプロジェクトへ偏りやすいという指摘。
- 持続的な資金源: Optimism は手数料収益で賄うが、他チェーン・コミュニティでは[[財源設計]]が課題。

まとめ
Retroactive Public Goods Funding は「結果を見てから資金を配る」ことで公共財支援を効率化しようとする Vitalik の提案であり、[[Optimism]] の [[RetroPGF]] で大規模実装が進んでいます。評価体制の拡充や指標の標準化が次の課題ですが、QF や他のインセンティブ設計と組み合わせることで、Web3 エコシステム全体の公共財サステナビリティを底上げする鍵となりつつあります。


[Retroactive Public Goods Funding. Note: The Optimism team has long been… | by Optimism | Optimism PBC Blog | Medium](https://medium.com/ethereum-optimism/retroactive-public-goods-funding-33c9b7d00f0c)

[Review of Optimism retro funding round 1](https://vitalik.ca/general/2021/11/16/retro1.html)
- [[retro funding]]

[Retroactive public goods funding](https://notes.andymatuschak.org/z2cqeazKJoESAvRiX8ZUuaoxRNwAYw24G3nS)

[/tkgshn/デジタル公共財を持続可能な形で運営する方法](https://scrapbox.io/tkgshn/デジタル公共財を持続可能な形で運営する方法)
[/tkgshn/公共財（OSS）にExitを与えるRetroactive Public Goods Funding](https://scrapbox.io/tkgshn/公共財（OSS）にExitを与えるRetroactive Public Goods Funding)
[/tkgshn/何が役に立つかよりも、何が役に立ったかについて合意する方が簡単](https://scrapbox.io/tkgshn/何が役に立つかよりも、何が役に立ったかについて合意する方が簡単)

- > <img src='https://scrapbox.io/api/pages/emoji/twitter/icon' alt='/emoji/twitter.icon' height="19.5"/> .@optimismPBC と @VitalikButerin が[[OSS]]を持続可能な形で運営するための方法として、「Retroactive Public Goods Funding」という方法を考えました。 ここでいう”[[Public Goods]]”というのはソースコードが公開されてることで[[正の外部性]]を持つ資産という概念です。
- >  	@[[tkgshn]] [November 25, 2021](https://twitter.com/tkgshn/status/1463781141538824194?ref_src=twsrc%5Etfw)
    - [[Public Goods]]([[公共財]])に対する[[Retroactive Funding]]

