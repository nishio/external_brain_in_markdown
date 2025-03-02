---
title: "Alexaスキル"
---

from [[Alexa Echo Pop]]

[[Alexa]]
- [[Alexaスキル]]を作る方法
    - [Alexaの知識がないところからスキルを作ってみた | DevelopersIO](https://dev.classmethod.jp/articles/firststep-alexa-skil-develop1/?utm_source=chatgpt.com)
        - 簡単そう
    - [Alexa | アレクサ | Alexaスキル開発トレーニング](https://developer.amazon.com/ja-JP/alexa/alexa-skills-kit/get-deeper/tutorials-code-samples/build-a-skill)
        - オフィシャル解説
    - [AlexaでchatGPTとおしゃべりできる 「helloGPT」を公開しました｜uramot](https://note.com/uramot/n/n333c2aa1f25c)
        - とりあえずこれを入れるか
        - [Amazon.co.jp: helloGPT : Alexa Skills](https://www.amazon.co.jp/-/en/uramot/dp/B0C1SQ111B)
        - へえー、こんな感じで公開されてレビューがつくのか、面白いな
    - [ChatGPT と会話できる Alexa スキルを作った](https://zenn.dev/kou_pg_0131/articles/alexa-skill-gpt)

[Alexa | アレクサ | Alexaスキル開発トレーニング](https://developer.amazon.com/ja-JP/alexa/alexa-skills-kit/get-deeper/tutorials-code-samples/build-a-skill#training-1)
- 公式ドキュメント
- 「ハロー」とかだとシステムの起動ワードが先に発動するので「わかりません」という言葉を探して起動ワードにする必要がある
    - 「マイスキル」という名前になった
- ハローワールドと話すカスタムスキルができた
- [Understand Custom Skills | Alexa Skills Kit](https://developer.amazon.com/en-US/docs/alexa/custom-skills/understanding-custom-skills.html)
- [Understand Smart Home Skills | Alexa Skills Kit](https://developer.amazon.com/en-US/docs/alexa/smarthome/understand-the-smart-home-skill-api.html)
- スマートホームスキルは単発コマンドしか通用しない代わりにAmazonが表記揺れキーワードなどをたくさん用意してくれてるというのが違いらしい
- なので僕が色々やるのはカスタムスキルで良いようだ

2025-02-07
- 開発者コンソールどこだっけとなった
    - [https://developer.amazon.com/alexa/console/ask](https://developer.amazon.com/alexa/console/ask)

2025-02-09
- 玄関に紙で貼ってた出かけるときの持ち物リストをAlexaスキルにした
