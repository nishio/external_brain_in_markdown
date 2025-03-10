---
title: "Flash Loan"
---

無担保で1億円借りて数秒で返すことが手数料9万円程度で実行可能なので、アービトラージの機会があればガンガン実行されるようになり[[流動性]]が高まっている、という話

[秒速で1億借りて返す ~Aave Flash Loan in Ropsten~ |by 菅野 裕也 |中程度 --- 秒速で1億借りて返す ~Aave Flash Loan in Ropsten~ | by Yuya Sugano | Medium](https://yuyasugano.medium.com/%E7%A7%92%E9%80%9F%E3%81%A71%E5%84%84%E5%80%9F%E3%82%8A%E3%81%A6%E8%BF%94%E3%81%99-aave-flash-loan-in-ropsten-ebef622760cd)
<img src='https://scrapbox.io/api/pages/nishio/claude/icon' alt='claude.icon' height="19.5"/>
- Flash Loanとは、[[DeFi]] (分散型金融) プロトコルが提供する[[無担保]]の[[短期ローン]]のことです。その主な特徴は以下の通りです。
    - 担保不要: 通常のローンとは異なり、Flash Loanでは担保を提供する必要がありません。
    - 超短期: 借り入れと返済はすべて1つのトランザクション内で行われます。つまり、数秒以内に完了します。
    - 同額返済: 借り入れた金額と全く同じ金額を返済する必要があります。金利はかかりませんが、手数料が発生することがあります。
    - 技術的知識が必要: Flash Loanを利用するには[[スマートコントラクト]]を開発する必要があるため、一定の技術的知識が求められます。
    - [[アービトラージ]]などに利用: 複数の取引所での価格差を利用した裁定取引など、大量の資金を一時的に必要とする取引にFlash Loanがよく利用されています。

Flash Loanを利用することで、大量の資金を一時的に調達し、それを利用して利益を上げることが可能になります。ただし、技術的なハードルが高く、また全てを1トランザクション内で完結させる必要があるため、リスクも伴います。現在、[[Aave]]、[[dYdX]]、[[Uniswap]]などの主要なDeFiプロトコルがFlash Loanの機能を提供しています。
