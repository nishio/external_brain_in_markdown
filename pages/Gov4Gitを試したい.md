---
title: "Gov4Gitを試したい"
---

2024-02-09
[[gov4git]]
- 管理者でない一般参加者としてPluralityBookのコミュニティには入ってるんだけど、やっぱり管理者の立場を体験しないとなーと思っていた
- が、Webサイトを見ても導入の仕方がよくわかんないなーと放置していた
- [https://github.com/gov4git/gov4git](https://github.com/gov4git/gov4git)
- > [gov4git](https://twitter.com/gov4git/status/1755663386682269769) Today we released a new website. Take a peek for an updated intro to our product and market stance [https://gov4git.org](https://gov4git.org) #AI_Alignment #AI_Policy #Community_Managementgov4git.org
- >  gov4git: Decentralized governance for git communities

- まずは本番ではなく小さい練習用ので
    - [https://github.com/nishio/otameshi_gov4git](https://github.com/nishio/otameshi_gov4git)

- [https://github.com/gov4git/gov4git/blob/v2/doc/USER.md](https://github.com/gov4git/gov4git/blob/v2/doc/USER.md)
- >  member / organizer
    - というらしい
    - >  一般参加者 / やっぱり管理者の立場を体験しないとな
- [https://github.com/gov4git/gov4git/blob/v2/doc/ORGANIZE.md](https://github.com/gov4git/gov4git/blob/v2/doc/ORGANIZE.md)
    - > The first responsibility of the organizer is to deploy the governance system. This task is documented in the Deployment Guide.
    - >  Once the governance system is up and running, the organizer is responsible for governing the day-to-day function of the community, as described in the Governance Guide.

- [https://github.com/gov4git/gov4git/blob/v2/doc/DEPLOY.md](https://github.com/gov4git/gov4git/blob/v2/doc/DEPLOY.md)
    - Go install / add to PATH / clone repos
    - `$ go get github.com/gov4git/gov4git/gov4git@latest`
:

```
...
go: added github.com/gov4git/gov4git v1.1.15
% gov4git version
zsh: command not found: gov4git
```

- どこにインストールされたのか？？

> [hnakamur2](https://twitter.com/hnakamur2/status/1755949197889847436) `go install ...`とすると
>  ~/go/bin/gov4git
>  にインストールされます。
> [hnakamur2](https://twitter.com/hnakamur2/status/1755949588727697584) Go 1.17から実行ファイルのインストールには go install が必要となっています。
>  [Deprecation of 'go get' for installing executables - The Go Programming Language](https://go.dev/doc/go-get-install-deprecation)
> [nishio](https://twitter.com/nishio/status/1755950378724557241) ありがとうございます！できました！

:

```
% ~/go/bin/gov4git version
{
   "version": "v1.1.15",
   "revision": "",
   "last_commit": "0001-01-01T00:00:00Z",
   "dirty_build": true
}
```


> The governance automation — invoked by the GitHub action — executes on behalf of a dedicated GitHub user, which represents the governance system itself. You must create a new GitHub user, designated as the governance automation user — and name it appropriately, as it will speak to the community users via GitHub comments.
>  For instance, the Plurality Book Project — @pluralitybook on GitHub — uses a dedicated user called Plurality Book DAO — @pluralitybook-dao on GitHub — to operate the governance system.
account
- otameshi-dao

>  Invite the automation user to your organization with Owner privileges.
organization
![image](https://gyazo.com/eb46ebc97c5fd13f168839613bd38e29/thumb/1000)

![image](https://gyazo.com/8b0970baf8aa9fcc5af9396214a84d92/thumb/1000)

![image](https://gyazo.com/eca9ce2444e81f104052ec27a4ce8886/thumb/1000)
- これ？

![image](https://gyazo.com/a45488271383ed291d0f34f9fdb2f687/thumb/1000)
- これか

![image](https://gyazo.com/6820102f5ea21c2464e85cb7b5e9fb5d/thumb/1000)

> Under "Organization permissions" make the following choices:
- これが見つからない

> Deploy governance for your project repository
>  You are now ready to deploy governance on your project repository. This can be accomplished with a single command:

$GOV4GIT_RELEASE
v2.1.3


> 403 You need admin access to the organization before adding a repository to it.

![image](https://gyazo.com/96b028c8341f556ebb33f9eee5f17fcb/thumb/1000)

---
repos先に作る？
[https://github.com/otameshi-gov4git-org/first-test-repos](https://github.com/otameshi-gov4git-org/first-test-repos)
作った
> 403 You need admin access to the organization before adding a repository to it.
関係なさげ
