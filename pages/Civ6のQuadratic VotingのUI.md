---
title: "Civ6のQuadratic VotingのUI"
---

[[Voice Credit]]が[[継続価値]]を持っているタイプの(=本来の形の)[[Quadratic Voting]]の実装例
- 文脈: [[Quadratic VotingのUIの工夫]]
- Voice Creditが継続価値を持っていないタイプの例: [[RxC QV]]

[[Civilization VI: Gathering Storm]]の世界会議
![image](https://gyazo.com/d35cb1740aff6ea95458d20334a8d819/thumb/1000)

「外交的支持」がVoice Creditに相当する
0コストで1票投票した後で、追加でVoice Creditを支払うことによって票を追加できる
![image](https://gyazo.com/b3f396ad9a731a6e8d7340c967bdfc92/thumb/1000)

追加票が増えるごとに追加コストが一時関数的に増える
なので全体としては票数の二次関数的なコストが掛かる
![image](https://gyazo.com/18cd1e6cab26b7ea6b0752d9873c5c03/thumb/1000)

投票結果
1番と4番のプレイヤーがAに4票と5票を投じている。2番と3番のプレイヤーはBに投じている。
[[一人一票]]の投票なら同点だが、これはQuadratic Votingなのでコストを払ってたくさんの票を投じたプレイヤーの意見が通っている。
![image](https://gyazo.com/d395c3ca1a41d9a75518a02d08c2ba68/thumb/1000)
