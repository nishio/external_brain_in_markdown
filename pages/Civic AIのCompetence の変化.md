---
title: "Civic AIのCompetence の変化"
---

from [[Civic AI]]
Civic AIのCompetence の変化
<img src='https://scrapbox.io/api/pages/nishio/Claude/icon' alt='Claude.icon' height="19.5"/>
Competence の変化
二段階で起きています
1. 2026-02-18（commit 587b914）
- コミットメッセージは「move RLCF to Pack 4, add security to Pack 3」です。
- RLCF（[[コミュニティのフィードバックによる強化学習]]）は [[care-giving]] ではなく [[care-receiving]] に属する、という理由で Competence から Responsiveness へ移されました。[[trust-under-loss]] もこのとき RLCF と一緒に移っています。
- 空いた Competence に[[セキュリティ]]の段落が入り、Rule of thumb は「Security failures are moral failures.」になりました。言い切りの短い形です。

2. その後の言い回しの調整
:
| 日付 | Rule of thumb |
| -- | -- |
| 02-18 | Security failures are moral failures. |
| 02-21（a559c4c） | …are moral failures of those who build and deploy, not merely technical oversights. |
| 06-30（979d560） | …reveal moral failure in build and deployment before they read as technical oversights. |
「倫理の失敗である」から「倫理の失敗を露わにする」へ、少しずつ柔らかくなっています。
段落本文の例示も変わりました。最初の版は「scope creep」で、6/12 に「lateral movement」になっています。

流れとしての読み：マニフェストの初版は 2025-09 で、セキュリティを入れたのは約5か月後です。Audrey は 2025-09 の時点では、セキュリティを 6-Pack の中心に置いていなかったことになります。この後から加わった部分に触れる問いです。「なぜセキュリティを後から Competence に入れたのか」は、Audrey に聞ける自然なとっかかりになります。

