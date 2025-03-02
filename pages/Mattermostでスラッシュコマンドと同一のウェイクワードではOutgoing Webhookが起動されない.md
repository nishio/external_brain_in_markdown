---
title: "Mattermostでスラッシュコマンドと同一のウェイクワードではOutgoing Webhookが起動されない"
---

from [[Mattermostでチャットボット]]
[[Mattermost]]でスラッシュコマンドと同一のウェイクワードではOutgoing Webhookが起動されない
    - POSTで失敗するにしてもhttp.serverのログには記録が残るはずなのに残ってない
    - ngrokの表示にも出てこない
    - リクエストが飛んでいない疑惑
- [https://docs.mattermost.com/developer/webhooks-outgoing.html#troubleshooting](https://docs.mattermost.com/developer/webhooks-outgoing.html#troubleshooting)
    - > To debug outgoing webhooks in System Console > Logs, set System Console > Logging > Enable Webhook Debugging to true and set System Console > Logging > Console Log Level to DEBUG.
    - しかしこのログにも出ない
- スラッシュコマンドと同一のウェイクワードでは起動されないようだ
    - `/nisbot`と`nisbot foo`の両方を同時に使うことはできない
