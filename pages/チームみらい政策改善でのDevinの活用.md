---
title: "チームみらい政策改善でのDevinの活用"
---

[[チームみらい]]政策改善でのDevinの活用
後々面白い事例としてNoteの記事になりそうなので箇条書きでまとめておく
- 政策に対して1400+件のPRがある
    - [https://github.com/team-mirai/policy](https://github.com/team-mirai/policy)
    - [[いどばた政策立案]]モジュールがGitHubを直接使えない人でも提案できるようにした効果
- この全件を対象とする分析をしようとするとGithub APIのRate Limit (5000件 / hour)に当たる
- [[Devin]]に依頼するとWebブラウザで頑張って作業しようとしてしまう
- Github Actionsで毎時最新データを取得しJSONにするコードを書いた
    - [https://github.com/team-mirai/random/tree/main/pr_analysis](https://github.com/team-mirai/random/tree/main/pr_analysis)
    - これで毎時1000件のPRが来ても大丈夫
- データはここに置かれている
    - [https://github.com/team-mirai/policy-pr-data](https://github.com/team-mirai/policy-pr-data)
- Devinに日本語で指示することで、このデータを用いて全PRから特定条件のものを抽出してCSVにすることができた
    - Slackから指示して、結果のCSVはSlackに添付させる
    - 結果は2分で得られた
    - これによってエンジニアでない人でも「ある程度の実装が必要なタイプの分析」を24時間いつでも指示でき、数分で結果が得られる体制が整った
