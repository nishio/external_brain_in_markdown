---
title: "Looker StudioのMapは月間3万表示まで"
---

from [[日記2025-07-12]]
[[Looker Studio]]のMapは月間3万表示まで / [[地理情報]]
![image](https://gyazo.com/99ef7aedf566d964c5063fc03e22433a/thumb/1000)

![image](https://gyazo.com/d8d95d3738f57a293f47fe3f38b42fa3/thumb/1000)

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
Looker StudioでMapが表示回数エラーになったのでAPIキーを入れる
なにのKey？
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
Google Maps Platform の API キー（Maps JavaScript API が有効なもの） です。
なぜ必要？
Looker Studio の Google Maps チャートは、デフォルトでは共有キーで 月 3 万回まで 無料表示できます。上限を超えると「表示回数エラー」が出るため、自分のプロジェクトで発行したキーを指定して制限を外します。

> [nishio](https://x.com/nishio/status/1943833480892494211) チームみらいダッシュボードの地図が表示されなくなっていた問題を修正しました。無料だと月間3万viewの制限があったようなのでGCPでMap JavaScript APIを発行して設定しました。
>  ![image](https://pbs.twimg.com/media/Gvnh2akbsAICIs3?format=jpg&name=medium#.png)

---
費用調べたら思ったより高かった $7.00 / 1,000
数万円のコストがかかる見積もり
まあこれに関しては選挙期間中の時限的なものだから仕方ないよね

