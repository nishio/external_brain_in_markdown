---
title: "プロアクティブなSlack bot"
---

[[プロアクティブ]]な[[Slack bot]]

<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>
- Slackボットの実装を、従来の「メンションに反応する」リアクティブ方式ではなく、  イベントをキューに蓄積し、AIエージェントが余裕のあるタイミングで順次処理する仕組みにする設計を検討。
- この仕組みは、[[協調的マルチタスク]]とプロアクティブな動作（定期実行タスクによる[[自律的なアクション]]）を実現するためのもの。
- Pythonのasyncioを用いたサンプルコードを提示し、[[Slack RTM API]]を利用してイベントを受信・処理する方法を説明。

[https://chatgpt.com/c/67aa052b-7964-8011-8fa7-c761602ef157](https://chatgpt.com/c/67aa052b-7964-8011-8fa7-c761602ef157)
