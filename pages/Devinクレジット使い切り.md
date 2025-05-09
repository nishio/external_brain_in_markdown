---
title: "Devinクレジット使い切り"
---

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
## ざっくり何が起きたか

1. ### 4 / 21――残クレジットに気づく
- 事前購入した Devin ACU が期限目前と判明し、従量課金に切り替える前に“最後のラッシュ”を決意。

2. ### 4 / 22――タスク投げ込み祭り
- 停滞していた Issue を大量に Devin に読み込ませ、行動計画→実装まで自動進行。レビューが終わる前に日付が変わり、投げた内容を把握できなくなるほど並列化。

3. ### 4 / 25–26――ACU 消費を加速
- ACU 使用量が168 → 192 へ増加。
- 11 並列セッションでバグ修正・機能追加・README 改善などを同時進行。
- 典型例: Netlify の peerDependencies 衝突を自動調査し、依存を更新して再デプロイ。
- Kozaneba ではユーザのバグ報告をそのまま渡すだけで修正完了。

4. ### 4 / 27――残 40 トークンの“使い切りプラン”
- ChatGPT から「静的解析・テスト自動生成・アーキ図生成などに充てよ」と提案を受け実行。最終的に ACU を消費しきり、従量課金モードへ移行。

---

## 引き出せる有益な知見

- ① “AI 向けに整形されたタスク”が鍵
    - 曖昧な Issue は Devin が迷走し、人間側の判断待ちになる。
    - Issue テンプレに目的／受入条件／制約を必ず書く。難しい問題は 「調査→分割」タスクとしてまず投げる。
- ② AI はバグ修正とリファクタに強い
    - 再現手順付きのバグ報告→即パッチ（Kozaneba）。静的解析・依存更新も高速。
    - 日々のバグ報告をテンプレ化してそのまま AI に渡すワークフローを常設。
- ③ 並列実行には“メタ管理”が必要
    - 投げたタスクを忘れ、進捗が不透明に。
    - Devin セッションを自動サマリしてダッシュボード化（Issue/PR 一覧＋状態）。
- ④ コードは“AI が触れる場所”に置く
    - 古い Heroku-only リポジトリは GitHub へ移す手間が発生。
    - 一元 VCS 化＋ README にセットアップ手順を残す。
- ⑤ 前払いクレジットは行動をゆがめる
    - “使い切り”のために低優先タスクまで着手。
    - 次回は 従量課金 or 小額前払い＋自動通知で無駄なラッシュを防ぐ。
- ⑥ 人間が担うべきは戦略とレビュー
    - 高度な意思決定は AI に丸投げ不可。
    - “AI→案出し / 人→決定”を徹底し、レビュー用チェックリストを用意。

日記
- [[Devinクレジット使い切り4/21]]
- [[Devinクレジット使い切り4/22]]
- [[Devinクレジット使い切り4/23棚卸し]]
- [[Devinクレジット使い切り4/25]]
- [[Devinクレジット使い切り4/26]]
- [[Devinクレジット使い切り4/27]]
- [[Devinクレジット使い切り振り返り]]
- [[Devinクレジット使い切り4/28]]
