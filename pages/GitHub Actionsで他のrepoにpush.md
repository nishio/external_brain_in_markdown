---
title: "GitHub Actionsで他のrepoにpush"
---

<img src='https://scrapbox.io/api/pages/nishio/Sonnet3.7/icon' alt='Sonnet3.7.icon' height="19.5"/>
GitHub Actionsから別のリポジトリにプッシュする際の403エラーは、デフォルトの`GITHUB_TOKEN`に他のリポジトリへのプッシュ権限がないことが原因です。

解決策：
1. GitHubで Personal Access Token (PAT) を作成
    - Settings → Developer settings → Personal access tokens → Generate new token (classic)
        - repoのsettingsではなく個人の方ね<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - ![image](https://gyazo.com/46e81de84b91fef5b2c467d1f97d1cf9/thumb/1000)![image](https://gyazo.com/528db934d891a1c8c2c5547688f4f322/thumb/1000)
        - 最低限`repo`スコープを付与
    - 生成されたトークンをコピー

2. リポジトリの Settings → Secrets → Actions で新しいシークレットを追加
    - 名前：`PAT`
        - 値：コピーしたトークン

3. ワークフローファイルを修正
yaml

```yaml
 name: Run update script
 run: |
  bash tasks/update_markdown/run.sh
 env:
  SID: ${{ secrets.SID }}
 GITHUB_TOKEN: ${{ secrets.PAT }}  # ここを変更
```


これで、GitHub Actionsが別のリポジトリにプッシュできるようになります。