---
title: "SlackとGitHubからのレポート生成"
---

Slack
- [https://x.com/nishio/status/1904480017335431447](https://x.com/nishio/status/1904480017335431447)
    - デジタル民主主義2030のSlack解説(2025-03-25)を生成しました
- 過去3日間の解説も生成してみた、　具体性が上がった
    - [https://gist.github.com/nishio/0a8ba0c3a1d7f7b6742966cafc0cf547](https://gist.github.com/nishio/0a8ba0c3a1d7f7b6742966cafc0cf547)
- 20時の定例に向けて、いどばたのものを参考に、共有事項ある方は各自こちらに記載いただけるとよいかと思っています。
    - [https://docs.google.com/document/d/1plggszRTxEEYUcZuCLiHkPrBsMtxr3RQpctKtZe5y4M/edit?tab=t.0](https://docs.google.com/document/d/1plggszRTxEEYUcZuCLiHkPrBsMtxr3RQpctKtZe5y4M/edit?tab=t.0)
    - 広聴AIのSlackだけから作ったもの

GitHub
- > 以下は、2025-03-20～2025-03-27の1週間に「digitaldemocracy2030/kouchou-ai」リポジトリで起きた主な出来事をかいつまんでまとめたものです。新機能やバグ対応が多数あり、プロジェクトが大きく進化しています。
- [https://gist.github.com/nishio/82918f0652a420352ccf84d67ce95562](https://gist.github.com/nishio/82918f0652a420352ccf84d67ce95562)


GitHub Actionでの
uses: nishio/gsheet-slack-logger@main
はnishio/gsheet-slack-logger@mainのリポジトリ内の action.yml に記述された定義に基づいて処理を行う

action.yml

```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
```


`$ docker build -t gsheet-slack-logger .`
`$ docker run --rm --env-file .env gsheet-slack-logger`

