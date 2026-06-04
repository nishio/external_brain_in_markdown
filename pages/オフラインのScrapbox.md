---
title: "オフラインのScrapbox"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>ScrapboxをObsidianに変換してオフラインで使い、オンラインになった後で更新されてるものだけアップロードすれば良い
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
全体像（最短ルート）
- Scrapbox ⇄ Obsidian を「同期」ではなく「片方向差分反映」にする
    1. Scrapbox → Obsidian（初回 or 定期）
    2. オフラインでObsidian編集
    3. オンライン復帰時：変更されたノートだけ Scrapbox に反映
- 👉 双方向リアルタイム同期はやらない（地獄を見る）

① Scrapbox → Obsidian 変換
これは既に前例が多いです。
- Scrapbox API で pages を取得
- 1ページ = 1 Markdown (`.md`)
結果：
_

```
vault/
 ├── PageA.md
 ├── PageB.md
 └── ...
```

👉 iCloud / Dropbox 配下に置けば iPhone 完全オフラインOK

② オフライン編集（iPhone）
- Obsidian iOS
- 完全オフラインで編集可
- 内部リンクもそのまま使える
ここで重要なのは：
- 「Scrapboxと同一視しない」
    - Obsidian側は思考のローカル作業場（dirty state OK）

③ 差分検出（ここが肝）
やるべきことは単純：
- Obsidian側で各 `.md` の`mtime`もしくは frontmatter に `last_modified`
- Scrapbox側でAPIの `updated` timestamp
- Obsidianで触ったものだけ上書き

④ Obsidian → Scrapbox 反映
- Markdown → Scrapbox 記法に逆変換
- Scrapbox APIで `PUT /pages/{project}/{title}`
注意点：
- Scrapbox側でオンライン中に更新されたページは 競合扱い
    - → 上書きしない
    - → 別ページに逃がす（`PageA (conflict YYYYMMDD)`）

実運用での思想（大事）
これは同期じゃなくて：
- Scrapbox = 正
- Obsidian = 作業コピー
    - オフライン時：Obsidianが主
    - オンライン復帰：Scrapboxに「成果だけ戻す」

たぶん西尾さん的にハマるポイント
- 「完全オフライン思考」が可能
- iPhoneでもリンク思考を維持
- 後段で
    - AIでページ分割
    - AIでタグ補完
    - AIで公開用整形
が自然に挟める