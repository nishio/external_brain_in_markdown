---
title: "Looker Studioで読めるJSON構造"
---

[[Looker Studio]]はJSONが読めるので[[Gist as GET API]]したら楽ちん！と思ったが素朴なJSONは読めないことがわかった
NG.json

```json
{
  "total_contribution_prs": 72,
  "daily_counts": {
    "2025-06-09": 11,
    "2025-05-22": 9,
    ...
  },
  "generated_at": "2025-06-10T05:32:26.282510Z"
}
```

OK.json

```json
{
  "total_contribution_prs": 72,
  "daily_counts": [
    {"date": "2025-05-15", "count": 5},
    {"date": "2025-05-16", "count": 3},
    {"date": "2025-05-18", "count": 6},
    ...
  ],
  "generated_at": "2025-06-10T13:47:41.871113Z"
}
```

後者のスタイルにしてroot elementをdaily_countsだと指定してやることで、テーブル型のデータソースとして扱えるようになる

next: [[Looker Studioで日付をDate型にしないとグラフにできない]]
