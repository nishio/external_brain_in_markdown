---
title: "VSCode Remote ターミナル永続化"
---

[https://gist.github.com/nishio/85a7380a8567daf1760d5f8be5e12d85](https://gist.github.com/nishio/85a7380a8567daf1760d5f8be5e12d85)
[[VS Code Remote Development]] ターミナル永続化
[[tmux]]

<img src='https://scrapbox.io/api/pages/nishio/codex/icon' alt='codex.icon' height="19.5"/>
Remote側に以下を作成済みです。 /home/ubuntu/.vscode-server/data/Machine/settings.json
内容は、新規VS Code terminalを `/usr/bin/tmux new-session -A -s vscode-${workspaceFolderBasename}` で起動し、task/debug用terminalは通常の /bin/bash -l に逃がす設定です。JSON妥当性とtmux起動も確認済みです。
