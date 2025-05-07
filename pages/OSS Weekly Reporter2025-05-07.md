---
title: "OSS Weekly Reporter2025-05-07"
---

お、GitHub Actionsが無事走りきってるみたい
[https://github.com/nishio/oss_weekly_reporter/actions/runs/14874435303](https://github.com/nishio/oss_weekly_reporter/actions/runs/14874435303)

ダメだ、Slackしかできてないぞ
- ローカルでSlack以外の部分を実行
    - GitHub部分はOK
    - > GitHub CLIからトークンを取得できませんでした: Command `'['gh', 'auth', 'token']'` returned non-zero exit status 1.
    - 全然ダメじゃん
- `$ python -m src.call_openai_api slack --all-summary`
    - チャンネル名が変わってskip channelが外れてるな
    - 直した


