---
title: "Looker Studioで日付をDate型にしないとグラフにできない"
---

[[Looker Studio]]で日付を[[Date型]]にしないとグラフにできない

"ディメンジョンが無効です"というエラーになる
- 日付が"2025-01-01"みたいな文字列のままでは理解できないようだ
- 折れ線グラフだけみたい

o3は「[[ISO 8601 日付]] 2025-05-15 年4桁‐月2桁‐日2桁（ハイフン区切り）。Looker Studio が最も確実に判定します。」っていうけど認識しないw
- 結局、計算フィールドで`PARSE_DATE('%Y-%m-%d', date)`するのが一番手っ取り早い

関連
- [[LookerStudio文字列型のままではマップ集計できない]]
