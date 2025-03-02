---
title: "git update-index --skip-worktree"
---

[[.vscode/settings.json]] が既に存在していて共同開発のrepoにある状態で、自分のローカルの.vscode/settings.jsonを編集すると「[[未コミットの変更]]がある」という状態になりpullの際に[[毎回stashが必要になる]]のが問題、どうしたらいい？

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>git update-index --skip-worktree を使う
- 利点: ローカルの設定ファイルを変更しても、Gitがその変更を追跡しなくなります。
- 手順:
    - 以下のコマンドを実行して、特定のファイルの追跡を無効にします:
    - `$ git update-index --skip-worktree .vscode/settings.json`
- これにより、ローカルの設定を変更してもGitがそれを検出せず、コミットの対象から外れます。
- もし変更を再度追跡したい場合は、以下のコマンドで無効化を解除できます:
    - `$ git update-index --no-skip-worktree .vscode/settings.json`
- この方法で、ローカルの設定を維持しつつ、リポジトリとの衝突を防げます。


なるほど〜〜<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

[[Denoではなくnpmを使う]]
