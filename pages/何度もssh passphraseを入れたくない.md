---
title: "何度もssh passphraseを入れたくない"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>How can I avoid to enter ssh-key passphrase repeatedly in console or Visual Studio Code?
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>
- `$ eval "$(ssh-agent -s)"`
- `$ ssh-add ~/.ssh/id_rsa`

[[GPT4に技術を聞く]]
