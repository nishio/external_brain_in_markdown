---
title: "GPT4かGPT3.5かを見分ける"
---

> [ActiveTK5929](https://twitter.com/ActiveTK5929/status/1640713653564604418/photo/1) ...ところで、AI自身は「自分はGPT-3である」と認識されているようですが、これはOpenAI側の問題でしょうか・・。
>  ![image](https://pbs.twimg.com/media/FsT8GePaQAEMk04?format=png&name=small#.png) ![image](https://pbs.twimg.com/media/FsT8IMraYAIu_ks?format=png&name=small#.png)
> [nishio](https://twitter.com/nishio/status/1640714763654303745) APIではgpt-4を指定しているのですが、どうやら自分のことをGPT3だと認識してるみたいですね。何かGPT3かGPT4かを確実に識別できるプロンプトがあればいいのですけど…。

by Kengo Nakajima
![image](https://gyazo.com/bb2e34644d87aeefc185c752fc21cc90/thumb/1000)

本家ChatGPTで試す
- GPT3.5
    - ![image](https://gyazo.com/1d002c9f6a112d3d6bb3cfa4c99ab628/thumb/1000)
    - 不等式定理に言及してるのに、自信満々で「満たしてる」と言ってて「知識のあるアホ」ですね
- GPT4
    - ![image](https://gyazo.com/5539e3f93742db9f498ce3d7c254f58a/thumb/1000)
    - 三角形が作れないことをちゃんとわかってる

この質問について
- ![image](https://gyazo.com/caf8d088da79853c0fd1cd756a218e99/thumb/1000)
- 本家ChatGPTではこう答える
    - ![image](https://gyazo.com/41cbee0c66852301d1201f7e3bfb1bb5/thumb/1000)
    - たぶんシステムプロンプトに「あなたはGPT-4をベースにしてOpenAIが開発したChatGPTです」とか書いてあるんだろう
