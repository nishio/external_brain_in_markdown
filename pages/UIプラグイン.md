---
title: "UIプラグイン"
---

<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>主にTypeScriptで作られている(ReactのUIコンポーネントなど)をプラグインとして配布するにはどういう構造が良い？
<img src='https://scrapbox.io/api/pages/nishio/GPT5/icon' alt='GPT5.icon' height="19.5"/>TypeScript（ReactのUIコンポーネント含む）を「プラグイン」として配布するなら、だいたい次の3パターンのどれかに寄せるのが安定です。結論としては 「UIコンポーネント +（任意で）manifest」= npm配布、ホスト側は動的importで読み込む が一番筋が良いです。
[https://chatgpt.com/c/6981cf4f-90b0-83a3-84d1-a73f9d9ef310](https://chatgpt.com/c/6981cf4f-90b0-83a3-84d1-a73f9d9ef310)
