---
title: "Talk to the Cityのexpandedの意味"
---

<img src='https://scrapbox.io/api/pages/nishio/o1 Pro/icon' alt='o1 Pro.icon' height="19.5"/>"expanded"は、ツールチップ（ホバーツールチップ）の表示状態を管理するためのstateです。
コード内では、
- 通常、マウスホバーなどでツールチップが表示されるが、"expanded"がfalseのときはカーソル移動でツールチップが消える状態
- "expanded"がtrueの場合は、ユーザーがクリックなどでツールチップを固定表示状態にし、その後さらにクリックすると再び非表示に戻せる状態
といった挙動を実現しています。

まとめると、"expanded"はツールチップが一時的なホバー表示ではなく、固定展開表示されているかどうかを示すフラグとして使われています。


