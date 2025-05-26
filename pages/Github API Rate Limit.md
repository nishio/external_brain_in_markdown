---
title: "Github API Rate Limit"
---

o3調べ
<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
- GitHub Actions から GitHub API を呼ぶ場合、どのトークンで認証するかによって一次レート制限（primary rate limit）の「範囲」と上限が変わります。
    - GITHUB_TOKEN（デフォルト）: リポジトリ単位で 1 000 リクエスト/時。同じリポジトリ内のすべてのワークフロー／ジョブがこのバケットを共有します。
    - Personal Access Token / OAuth access token: ユーザー単位で 5 000 リクエスト/時（Enterprise Cloud 組織所有なら 15 000 リクエスト/時）。
