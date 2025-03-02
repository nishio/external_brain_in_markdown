---
title: "git@github.com: Permission denied (publickey)"
---

VSCode
> Error: Unable to Fetch from Remote(s)
>  git@github.com: Permission denied (publickey).
>  fatal: Could not read from remote repository.
>  Please make sure you have the correct access rights
>  and the repository exists.
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>どういうこと？
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
このエラーは、GitHubリポジトリにアクセスする際にSSH認証が失敗したことを意味します。以下のような原因が考えられます。
2. SSHエージェントが鍵を読み込んでいない
- SSHキーがエージェントに追加されていない場合、GitHubへのアクセスが拒否されます。
- エージェントを起動:
    - `$ eval "$(ssh-agent -s)"`
- 鍵を追加:
    - `$ ssh-add ~/.ssh/id_rsa`

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>再発防止は？

<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
3. Macの場合: macOS専用の設定
macOSではキーチェーンにSSHキーを登録しておくと、ログイン時に自動で読み込まれます。
SSHキーをキーチェーンに登録：
- `$ ssh-add --apple-use-keychain ~/.ssh/id_rsa`
~/.ssh/config に以下を追加：
:

```
Host *
   UseKeychain yes
   AddKeysToAgent yes
   IdentityFile ~/.ssh/id_rsa
```



---<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
[[~/.ssh/config]] に既にこう書かれてたので[[ssh-agent]]が自動起動してなかったのが原因かな
:

```
Host github
  AddKeysToAgent yes
  UseKeychain yes
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa
```

