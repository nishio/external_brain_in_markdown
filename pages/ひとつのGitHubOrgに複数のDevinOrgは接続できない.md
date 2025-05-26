---
title: "ひとつのGitHubOrgに複数のDevinOrgは接続できない"
---

![image](https://gyazo.com/3a14f1bd52fde78842437d2b570146da/thumb/1000)
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
- Devin の GitHub 連携は GitHub App としてGitHub Organizationにインストールされ、そのインストール ID が 1 つの Devin Organization（テナント）に結び付きます。
- このため 同じ GitHub Organization に「複数の Devin Organization」を同時に接続することはできません。
- 既に接続済みの Devin Organizationがある場合は、先にその連携をアンインストールしてから別の Devin Organizationを接続し直す必要があります。
- 逆に、1 つの Devin Organization内ではメンバーが何人でも・セッションをいくつでも並行実行できますので、通常のチーム開発で困ることはありません。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- まあメインの組織の外側にパーミッションレスなボランティア組織がある開発形態は「通常のチーム開発」じゃないってことだよな
- 方針
    - team-mirai-volunteersみたいなorgを新しく作る(長いので以下tmv)
    - DevinがtmvにPRを作ったとしても、それをteam-miraiにmergeすることはできる
    - tmvにはteam-miraiが更新されたらpullするGithub Actionを入れとけばいいのではと思う

