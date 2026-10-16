---
title: "ショートカットキーでneologd.normalize"
---

![image](https://scrapbox.io/files/6ad18ce76bd7d205ec7eaa8f.png)
Automatorでこんな感じのサービスを作って、キーボードの設定からショートカットキーを割り当てる

/usr/local/bin/python3 -c "import nelogdn, sys; sys.stdout.write(neologdn.normalize(sys.stdin.read()))"

[[neologdn]]はあらかじめpython3にいれてあるとする
