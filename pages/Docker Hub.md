---
title: "Docker Hub"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>今、[[Docker Desktop]]をMacで使っていて、特に気にすることなくdocker pullできています。Ubuntuの環境で同じことをやったらunauthorized pullのrate limitに引っかかりました。どうしたらいい？

<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>Docker Hub では、認証済みと未認証でpullの制限が異なります。Mac の Docker Desktop は内部で認証情報を利用しているため、rate limit に達しにくいですが、Ubuntu では未認証の状態になっている可能性があります。対策として、Docker Hub のアカウントを作成し、Ubuntu 上で以下のコマンドを実行して認証してください。
`$ docker login`
これにより、認証済みの状態となり、pull 制限が緩和されます。さらに、必要に応じて有料プランも検討すると良いでしょう。