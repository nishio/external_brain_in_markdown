---
title: "Blenderを例に見るOSSプロダクト継続性の仕組み"
---

[[Blender]]を例に見る[[OSS]]プロダクト[[継続性]]の仕組み

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
## Blenderを例に見るOSSプロダクト継続性の仕組み

### 1. 歴史 – 「Free Blender」から始まった継続性の土台

* 2002年、商用版 Blender を開発していた NaN 社が倒産。創始者 Ton Roosendaal はソースコードと商標を買い戻すには 10 万 € が必要と投資家に交渉し、コミュニティとともにクラウドファンディング **“Free Blender”** キャンペーンを実施。わずか7週間で目標額を達成し、GPL で公開されたことが現在の OSS 体制の出発点となった ([[docs.blender.org]][[1]])。

### 2. ガバナンス構造

| 組織                             | 役割                                 | 継続性への寄与                           |
| ------------------------------ | ---------------------------------- | --------------------------------- |
| **Blender Foundation**         | 法人格・商標管理・寄付受け皿                     | 中立性と信頼の確保                         |
| **Blender Institute / Studio** | コア開発者雇用、LTSビルド・ドキュメント整備、オープンムービー制作 | フルタイム開発者の安定雇用／新機能検証               |
| **Developer モジュール制**           | コードオーナーを明示し、レビューとロードマップをモジュール単位で管理 | ナレッジ集中を防ぎバス係数↑ ([[blender.org]][[2]]) |

### 3. 資金モデル

| 主な流入                                | 仕組み                | 最新規模                                                                                |
| ----------------------------------- | ------------------ | ----------------------------------------------------------------------------------- |
| **月額寄付 Development Fund**           | 個人・企業のサブスク         | 月額 **約 25.5 万 USD**、個人 7 575 口・企業 38 社 (2025‑07 時点) ([[Blender Development Fund]][[3]]) |
| **企業会員（Bronze 6k€ → Patron 240k€）** | 特典は名称掲載・開発窓口など     | 階層設計で多様な企業が参加 ([[Blender Development Fund]][[4]])                                       |
| **Blender Studio サブスク / グッズ販売**     | オープンムービー素材・チュートリアル | 開発者雇用の追加財源                                                                          |
| **助成金・一括寄付**                        | Epic MegaGrant 等   | リスク分散                                                                               |

>  年間寄付総額は 2022 年 2.17 M→2023 年 2.55 M→2024 年 2.93 M USD と右肩上がり ([[Reddit]][[5]])。Foundation 年報でも 2023 年収入 2.5 M €・前年比 +20 % と報告 ([[download.blender.org]][[6]])。

### 4. リリース戦略

* **四半期リリース**：通常版は約4 か月ごと。
* **年次 LTS**：毎年 1 本を2年間メンテ。例）4.2 LTS（2024‑07‑16）([[blender.org]][[7]])、**最新安定版 4.5 LTS（2025‑07‑15）** ([[blender.org]][[2]])。
* 明確なカレンダーでユーザーの業務ツールとしての信頼性を確保。

### 5. コミュニティとエコシステム

* **コード貢献**：モジュール制 + RFC/Code Review で質と速度を両立。
* **Add‑on 市場**：GPL 互換を保ちつつ、外部サイトで商用販売可能。エコシステムの経済圏が開発者を呼び込む。
* **オープンムービー**：実運用で新機能をテストし、成果物を無償公開。マーケティングと QA を兼ねる。

### 6. 継続性を支える要因

1. **コミュニティ主導の“所有”感**

        - * 初期に「買い戻し」を支えた当事者意識が今も寄付文化として残る。
2. **多層的な収益構造**

        - * 小口寄付＋企業会員＋制作スタジオ＋グッズで“単一スポンサー依存”を回避。
3. **中立的ガバナンス**

        - * 財団と商標の分離により、いかなる企業にも過度に左右されない。
4. **プロダクト管理の透明性**

        - * 公開ロードマップ・議事録・リリースサイクルが明確で、長期利用計画を立てやすい。
5. **ユーザー価値への一貫投資**

        - * UX 改善や LTS 保守に資金を優先配分し、「無料だから不安」を払拭。

### 7. OSS プロダクト継続のヒント（Blenderから学べること）

* **資金源を“寄せ木細工”に**：少額の裾野を広げつつ、大口スポンサーには明確な見返りを提示。
* **ガバナンスを透明化**：権限と責任を文書化し、コミュニティが監視できる仕組みを用意。
* **実プロジェクトで“食べる”**：Blender Studio のように OSS を使った制作事例を自ら作り、改良サイクルを早める。
* **長期サポート版の提供**：業務利用者が安心して投資できる環境を整える。
* **ブランドとストーリー**：Free Blender の物語が“寄付したくなる理由”を今も提供している。

---

Blender は「コミュニティが買い戻したソフト」を出発点に、明快なガバナンスと多層的な収益モデルを築くことで、20年以上プロダクトを進化させ続けている好例と言えます。自社プロダクトを OSS 化したい場合も、**資金・ガバナンス・リリース戦略をセットで設計すること**が継続性の鍵になります。

[[1]]: [https://docs.blender.org/api/htmlI/x115.html?utm_source=chatgpt.com](https://docs.blender.org/api/htmlI/x115.html?utm_source=chatgpt.com) "Blender's History"
[[2]]: [https://developer.blender.org/docs/release_notes/](https://developer.blender.org/docs/release_notes/) "Blender Release Notes - Blender Developer Documentation"
[[3]]: [https://fund.blender.org/](https://fund.blender.org/) "Blender Development Fund"
[[4]]: [https://fund.blender.org/corporate-memberships/](https://fund.blender.org/corporate-memberships/) "Corporate Memberships — Blender Development Fund"
[[5]]: [https://www.reddit.com/r/blender/comments/1huo9nw/regarding_the_recent_news_about_blender_lack_of/?utm_source=chatgpt.com](https://www.reddit.com/r/blender/comments/1huo9nw/regarding_the_recent_news_about_blender_lack_of/?utm_source=chatgpt.com) "Regarding the recent news about Blender lack of funding, I made ..."
[[6]]: [https://download.blender.org/foundation/Blender-Foundation-Annual-Report-2023.pdf?utm_source=chatgpt.com](https://download.blender.org/foundation/Blender-Foundation-Annual-Report-2023.pdf?utm_source=chatgpt.com) "[[PDF]] Blender Annual Report — 2023"
[[7]]: [https://developer.blender.org/docs/release_notes/4.2/?utm_source=chatgpt.com](https://developer.blender.org/docs/release_notes/4.2/?utm_source=chatgpt.com) "Blender 4.2 LTS Release Notes - Blender Developer Documentation"
