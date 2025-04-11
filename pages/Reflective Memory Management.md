---
title: "Reflective Memory Management"
---

[[In Prospect and Retrospect: Reflective Memory Management for Long-term Personalized Dialogue Agents]]
[https://arxiv.org/pdf/2503.08026](https://arxiv.org/pdf/2503.08026)
<img src='https://scrapbox.io/api/pages/nishio/GPT-4.5/icon' alt='GPT-4.5.icon' height="19.5"/>
# 論文の概要
長期間にわたってユーザーとの会話を継続し、過去の情報を正確に記憶・利用するための新たな記憶管理手法「Reflective Memory Management (RMM, [[反省的記憶管理]])」を提案。RMMは以下2つの要素から成る：

- Prospective Reflection（前向きの内省）
- 会話終了後に対話内容をトピック単位で分解・要約し、意味的にまとまった記憶として整理する。これにより固定された単位（ターンやセッションなど）による記憶の断片化を防ぐ。

- Retrospective Reflection（後向きの内省）
- 会話生成時にLLM自身が「どの記憶が役に立ったか」を自動で評価。その評価を強化学習の報酬として、記憶の検索結果をオンラインで改善・調整する。

# 従来手法の課題
- 固定的な粒度の記憶管理：ターンやセッション単位の固定された区切りでは意味的なまとまりを捉えられず、記憶が断片化・不完全になる。
- 固定的な記憶検索手法：ユーザーや対話状況の多様性に対応できない。

# 提案手法（RMM）のメリット
- トピックベースで記憶を管理し、意味的なまとまりを保持することで、記憶検索の精度を向上。
- 検索された記憶の役立ち度合いをLLM自身が判定することで、ラベル付けデータなしで記憶検索の精度をオンラインで改善できる。

# 実験結果
- MSCおよびLongMemEvalのデータセットで検証。
- 提案手法は既存のベースラインより精度が高く、特にLongMemEvalデータセットでは記憶管理を使わない場合と比較して、正解率が10%以上向上。

# 結論・今後の課題
- RMMは長期的なパーソナライズ対話エージェントにおいて優れた精度を示した。
- 今後の課題として、計算効率化、多モーダル対話への対応、個人情報保護の強化が挙げられる。

---

以上が論文の要点をコンパクトにまとめたものです。


関連
- [[MemoChat]]
- Survey [https://chatgpt.com/c/67e139ac-05fc-8011-a6d8-d6887700b11b](https://chatgpt.com/c/67e139ac-05fc-8011-a6d8-d6887700b11b)
    - [[Keep Me Updated]]
    - [[MemoryBank]]
