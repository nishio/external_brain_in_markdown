---
title: "zshで#をコメントにする"
---

<img src='https://scrapbox.io/api/pages/nishio/o3-mini-high/icon' alt='o3-mini-high.icon' height="19.5"/>zsh でも bash と同じく、コメント行として「#」を使うのが基本です。ただし、インタラクティブシェルで直接入力する場合、setopt interactive_comments を有効にしていないと、# から始まる行がコマンドとして解釈されることがあります。

インタラクティブシェルでコメント行を入力してもコメントとして認識させたい場合、`setopt interactive_comments` を .zshrc に追加すると、bash と同じように動作します。

[[zsh]]
