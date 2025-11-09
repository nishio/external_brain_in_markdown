---
title: "VSCodeのshellをzshにする"
---

[[VSCode]]のTerminal開始時にこれが出る
:

```
The default interactive shell is now zsh.
To update your account to use zsh, please run `chsh -s /bin/zsh`.
For more details, please visit https://support.apple.com/kb/HT208050.
```


<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
そのメッセージは bash を起動したとき macOS が出す定型文です。
macOS Catalina 以降の “推奨シェル” が zsh になったため、まだ bash を使っているユーザに「chsh -s /bin/zsh で切り替えられますよ」と案内しています。
VS Code のターミナルで bash が起動すると毎回表示されますが、実害はありません。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>実がいなくてもウザいし、そもそもOSをupdateしたわけではないのになんで出るようになった？Claude Codeのせい？

<img src='https://scrapbox.io/api/pages/nishio/o3/icon' alt='o3.icon' height="19.5"/>
VS Code 側でデフォルトシェルを指定する方法
⌘, で設定を開く → 「Terminal › Integrated: Default Profile (mac)」を検索。

ドロップダウンから zsh を選択。

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
![image](https://gyazo.com/2321546ca02018cef422be8608f578d0/thumb/1000)
まあこれを直しておくか
