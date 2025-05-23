---
title: "Macのメニューバーに入るポモドーロタイマー"
---

Macのメニューバーに入る[[ポモドーロタイマー]]
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
選び方のヒント
- 細かな統計やアプリブロックが欲しい → Flow が最も多機能。Pro を買うと CSV で履歴出力も可能。
- 超軽量・すぐ始めたい → Horo は⌘+Space → horo 25m と打つ感覚で使える。
- タスク管理も一緒にやりたい → Be Focused（単体完結）か PomoDoneApp（他ツール連携）を。
- 追加課金なしでサッと試す → macOS Shortcuts で「タイマー開始」「休憩開始」を作ってメニューバー常駐させれば、無料でポモドーロ運用が可能。
※すべて Apple Silicon（M1/M2/M3）対応を確認済み。App Store 版は日本語 UI も含まれます。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[macOS Shortcuts]]でどうやるのか気になる

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
## macOS ショートカットで〈無料ポモドーロ〉を作る手順
（Sonoma 以降で確認。Ventura でもほぼ同じです）
## 1. 「集中開始」ショートカットを作る
1. ### ショートカット.app → ＋
 をクリックし、名前を
- `Pomodoro 25`（例）とする
2. 右上 `i` ボタン → ### “メニューバーにピン”
 をオン
3. 下記アクションを順に追加
1. タイマーを開始
        - `25` 分
2. （任意）集中モードを設定 → “おやすみモード”を 30 分間
    3. 通知を表示 → 「25 分集中スタート」
4. 待機 → `1500` 秒（＝25 分）
    5. 通知を表示 → 「お疲れさま！」
6. サウンドを再生 → “Glass” など

これ一本で「集中→通知→休憩へ」の流れまで完結します。
(連鎖して休憩タイマーを走らせる説明もあったが割愛)

## 3. さらに快適にする小技

- ⌘⌥P などで瞬時に開始
    - `i` ボタン → キーボードショートカットを設定
- 終わったら音楽を流す
    - 「ミュージックで再生」アクションを追加
- 自動ログを残す
    - 「現在の日付を取得」→「CSV に追記」→ `~/Documents/pomo.csv` 保存
- 毎朝自動で 1 回目を開始
- | 「オートメーション」→ “時刻” で 9 : 00 → 先ほどのショートカットを実行

## 4. 実行方法
- メニューバーに新しいアイコン 🟠 が出現 → クリックで実行
- Spotlight で `Pomodoro` と打って Enter でも OK
- 複数同時実行を避けたいときは、アクション「実行中なら終了」を先頭に挿入

これで専用アプリなしでも ### 完全無料・メニューバー常駐のポモドーロ環境
 が完成します。
もっと細かくカスタムしたい部分（ログ保存先の変更、通知文など）があれば教えてください！

---
Pomodoroタイマー作ってるメーカーの商売あがったりだなw<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
![image](https://gyazo.com/0d786b71e67e29b98617ea21f7e630c5/thumb/1000)


![image](https://gyazo.com/8fdbfd2ca1d51da51d40492a1f9e82a1/thumb/1000)![image](https://gyazo.com/a5fa08f7857bd40785af6dafda53b56c/thumb/1000)

