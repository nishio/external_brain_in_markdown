---
title: "ParsuaBot"
---

[2407.03585 Zero-shot Persuasive Chatbots with LLM-Generated Strategies and Information Retrieval](https://arxiv.org/abs/2407.03585?utm_source=chatgpt.com)
- EMNLP 2024: [https://aclanthology.org/2024.findings-emnlp.656.pdf](https://aclanthology.org/2024.findings-emnlp.656.pdf)

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
アーキテクチャ（Strategy Maintenance Module, SMM）
- LLM 応答生成
    - ユーザ入力とタスク指示を与え、GPT‑3.5 相当のモデルに“素”の説得メッセージを出させる。
- ストラテジー分割 & 抽出
    - 生成文を文脈的に分割し、各セグメントが用いる説得ストラテジー（例：影響強調・利益提示・共感表明など）を LLM に自己ラベル付けさせる。固定リストではなく動的生成。​
- 事実チェック＋IR 補強
    - 各セグメントの主張を検証。裏付けがないものは外部検索で信頼できるファクトを取得し置換。これにより説得構造は維持したままハルシネーションを除去。​
- マージ＆出力
    - 戻ってきた事実情報を各ストラテジー節へ埋め込み、自然な一本の回答として統合。

ポイント：ストラテジーと言語内容を分離して扱うため、どの主張を事実補強すべきか自動で判別できる。

寄付勧誘・旅行推薦・健康介入の3ドメインで同じパイプラインが機能し、タスク特化データや追加微調整は一切不要。
- 3領域×2種ユーザ（協力的 / 懐疑的）すべてで、先行手法より 平均 +0.6 ポイント高い説得スコアを記録。
    - (説得スコアとは80 名のクラウドワーカーが実際に対話し、各自1 回だけ5段階リッカート 1 = まったく説得されない … 5 = 非常に説得される で評価したもの)
