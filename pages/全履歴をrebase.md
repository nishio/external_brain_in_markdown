---
title: "全履歴をrebase"
---

正解は
- `$ git rebase -i --root`



<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>I want to `rebase -i` all history. How?
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
- `$ git rev-list --max-parents=0 HEAD`
- `$ git rebase -i <SHA>`

これは「ほぼ全部」だが、一番最初のroot commitは含まれない
- a,b,cとコミットした場合、上記の方法ではb,cがtodo listに出力される
- `$ git rebase -i --root`
    - これならa, b, cになる
