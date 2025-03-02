---
title: "OpenFisca"
---

[Write rules as code - OpenFisca](https://openfisca.org/en/)

[OpenFiscaについて | OpenFisca-Japan Docs](https://project-inclusive.github.io/OpenFisca-Japan/about_openfisca.html)
> OpenFiscaは、社会制度などをソフトウェアコードとして記述できる(Rule as Code)、フランス発のOSSです

[/tkgshn/OpenFisca](https://scrapbox.io/tkgshn/OpenFisca)

[What is OpenFisca? | Salsa Digital](https://salsa.digital/insights/what-is-openfisca)
- 各国事例

## LexImpact
- [/tkgshn/LaxImpact](https://scrapbox.io/tkgshn/LaxImpact)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>概要
[[LexImpact]]は、フランス国民議会が運用する社会・財政シミュレーターで、OpenFiscaを基盤に政策変更の影響を計算・可視化するツールです。市民や議員がシナリオを入力することで、税・社会保障制度の各種パラメータ（例：最低賃金、各種社会保険料など）の変更が与える影響をシミュレーションできます
- [Using AI to update OpenFisca parameters – update_openfisca_with_ai](https://documentation.leximpact.dev/ia/explication-en.html)

### 主な特徴
- シミュレーション機能
    - 政策変更（例：賃金改定や税率変更）の効果を迅速に計算し、結果をグラフィカルに提示します。これにより、議会内での政策議論や意思決定が支援されます。

- パラメータ管理と自動更新
    - OpenFiscaは多数の財政パラメータを扱いますが、LexImpactはこれらを最新の法改正に基づいて更新する仕組みを導入しています。具体的には、各パラメータに対して「値」「適用開始日」「法的根拠」などの情報が記録され、手作業では困難な大量更新を効率化しています。

- AI（大規模言語モデル）の活用
    - LexImpactでは、LLM（大規模言語モデル）を活用して、法令テキストから必要な数値や日付、法的参照情報を自動抽出する仕組みが導入されています。
    - ガイド付きLLMアプローチ：法令文とパラメータの説明を組み合わせ、LLMに正確な情報抽出を依頼します。
    - インテリジェントエージェントアプローチ：LLMがWeb検索やテキスト取得ツールを利用し、欠落した参照情報を補完する仕組みです.

### 意義と背景
- 政策評価の迅速化
    - 実際の制度変更前にその影響をシミュレーションできるため、政策立案や議会での検証プロセスが効率化されます。
- [[Rules as Code]]の具体例
    - 法律や規則をコード化するOpenFiscaの実装例として、LexImpactはAI技術と連携し、従来の手動更新から自動化への一歩を示しています.

以上のように、LexImpactはOpenFiscaの「法をコードにする」という考え方を実現する先進的なツールとして、政策シミュレーションおよびパラメータの自動更新において重要な役割を担っています。