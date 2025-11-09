---
title: "Bias for Action"
---


<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
Bias for Action（行動優先）
- 定義：不確実でも小さく早く動く姿勢。多くの意思決定は可逆なので、過度な分析より試行→学習→調整を重視する考え方。Amazonのリーダーシップ・プリンシプルの一つ。 ([amazon.jobs](https://www.amazon.jobs/content/our-workplace/leadership-principles?utm_source=chatgpt.com))
- 狙い：スピードで学習曲線を前倒しし、機会損失（待ち時間のコスト）を減らす。

[[Two-way door]]／One-way door
- 枠組み（Bezos）
    - One-way door = Type 1：不可逆（に近い）で影響大。ゆっくり慎重に、多面的に検討してから決める。
    - Two-way door = Type 2：可逆で影響限定。軽量プロセスで素早く試し、ダメなら戻す。 ([SEC](https://www.sec.gov/Archives/edgar/data/1018724/000119312516530910/d168744dex991.htm?utm_source=chatgpt.com))

実務での使い分け（最短手順）
1. 可逆性を判定
    - 低コストですぐ戻せる？→ Two-way（即実験）
    - 戻しづらい／法務・ブランド・安全に直結？→ One-way（入念に）
2. 影響範囲と待つコストを見積もる
    - 影響小×待つコスト大 → 先に動く
    - 影響大×待つ価値あり → 追加情報を集める
3. Two-wayの基本オペ
    - スコープ最小化 → ロールバック手順用意 → 期日付きの見直し基準（KPI/失敗条件）を先に決めて実行
4. One-wayの基本オペ
    - 代替案比較／プレモーテム／関係者レビュー／試験運用（可能なら）→意思決定

ありがちな失敗
- Type 2 を Type 1 と誤認→先延ばし・機会損失が増える（Bias for Actionで是正）。 ([アマゾンニュース](https://www.aboutamazon.com/news/company-news/2016-letter-to-shareholders?utm_source=chatgpt.com))
- Type 1 を Type 2 と誤認→回収不能のダメージ（Two-way判定を厳しめに）。 ([SEC](https://www.sec.gov/Archives/edgar/data/1018724/000119312516530910/d168744dex991.htm?utm_source=chatgpt.com))

ソフトウェア／研究での具体例
- Two-way例：UI文言変更、ランキング重みの微調整、ABテスト、小規模な内部ツール導入（明確なロールバック可）。
- One-way例：ライセンス変更、料金体系・契約条件の改定、データ削除を伴う移行、長期ロックインを招く基盤変更。

まとめ
- Bias for Actionは「まず動く」姿勢、Two-way doorは「まず動ける状況を見極める物差し」。
- 先に可逆性×影響×待つコストで分類し、Type 2は素早く、Type 1は慎重に――これが最短の運用ルールです。 ([amazon.jobs](https://www.amazon.jobs/content/our-workplace/leadership-principles?utm_source=chatgpt.com))
