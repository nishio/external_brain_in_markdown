---
title: "Chakra UI"
---

[[広聴AI]]で使われているUIコンポーネントライブラリ

[Chakra UI](https://chakra-ui.com/)

MUIなどと比べて何がいいのか教えて<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
<img src='https://scrapbox.io/api/pages/nishio/gpt5/icon' alt='gpt5.icon' height="19.5"/>ざっくり言うと、Chakra UI は “デザインに縛られない・学習しやすい・暗色対応が超ラク” なのが強み。MUI（Material UI）は部品がとても豊富で企業向け機能が強い。使い分けは目的次第です。
- Chakra が良いところ
    - デザイン中立：Material規格に寄らないので、自社デザインに合わせやすい（見た目の“素材”として扱える）。
    - APIの一貫性：size / variant / colorScheme と“スタイルprops”でほぼ統一。迷わず書け、TypeScriptの補完も効く。
    - ダークモードが標準装備：useColorMode() とトークンで、配色の切替が最短コスト。
    - レイアウトが直感的：Stack / HStack / VStack / SimpleGrid / Wrap で“余白と並び”をサクッと表現。
    - [[A11y]]と既定値が良い：フォーカス、キーボード操作、ARIAが最初から整っていて微修正で済む。
    - プロトタイピング速度：CSSを書かずに画面がすぐ組める → 小〜中規模SaaSやPoCに向く。
- 逆に MUI が強いところ
    - コンポーネントの裾野が広い：DataGrid・ピッカー類・Charts など“業務向け”が充実（一部有償）。
    - 資料と実例が豊富：Material/ Joy など複数デザイン体系、企業導入の知見が多い。
    - “Material準拠で早い”案件：UIルールが先に決まっているならMUIの方が手戻り少なめ。
