---
title: "npmを使用停止"
---

2025-09-25
- npmを全部使用中止にするとnpm devとかnpm testとかも使えなくて不便
- [[npm installだけを使用中止]]


2025-09-19
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>
目的が「しばらく“実行不可能”にする」なら、以下の順でおすすめします。
おすすめ順（macOS/Linux）

1. “ダミーnpm”をPATHの先頭に置く（安全・可逆）
:

```
mkdir -p ~/.bin
printf '#!/usr/bin/env bash\necho "npmは一時的に無効化中"; exit 127\n' > ~/.bin/npm
chmod +x ~/.bin/npm

シェル設定にPATH先頭を追加（bash例）
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.bashrc

zshなら
echo 'export PATH="$HOME/.bin:$PATH"' >> ~/.zshrc
exec $SHELL -l
which npm   # → ~/.bin/npm が出ればOK
```

既存のnpmは触らず、常にこのダミーが先に拾われるので壊しません。
解除は~/.bin/npmを削除するかPATH行を戻すだけ。

