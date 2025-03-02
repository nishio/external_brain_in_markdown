---
title: "GPT Builder"
---

GPT BuilderはGPTへの指示である「プロンプト」自体をGPTによって作るChatGPT Plusの機能
- プロンプトな書き方には、例えば「役割の明確化」とか「英語で書く」などのベストプラクティスがある
    - [[ユーザサイドのPrompt Engineering]]
- が、大部分のユーザはそれを学んで実行することができていない
- なのでGPT Builderでは「良いプロンプトを作る」というところ自体をGPTが支援する
- 日本語でやり取りしてもちゃんと英語のプロンプトを作ってくれるので英語の苦手な人も安心
    - ただしプロンプトに引きづられて英語で出力してくることがあるので、常に日本語で出力して欲しいならそう伝えるのが良い

![image](https://gyazo.com/14b9ecd91f3bacdfda87eb3da87aa33a/thumb/1000)

![image](https://gyazo.com/8e690de0fe80346029f481726c5a1791/thumb/1000)
- ![image](https://gyazo.com/2c64c58f0a38097ceb121d80b8e21d7f/thumb/1000)

日本語で指示を出す
- > 文章を与えられて、それを読んで「面白い」とか「よくわからない」とか「疑問がある」などの気持ちをいくつかの絵文字の列で表現するGPTを作って

![image](https://gyazo.com/937e238847de39c1a94a9c5c12989122/thumb/1000)

生成された設定
- ![image](https://gyazo.com/3cfdb322180fe8d2b0aa95b8d106c606/thumb/1000)
- > The GPT will be provided with text and will express feelings or reactions such as 'interesting', 'confusing', or 'questionable' through a series of emojis. It will read the given text and encapsulate the emotional response or opinion in emoji form, offering a unique and expressive way to convey reactions.

テスト実行
- ![image](https://gyazo.com/5e313a7903d29179fc3962397dfc1946/thumb/1000)
- 長い、そうじゃない
- > 主要な感情を冒頭の数個に入れてください。長すぎないように、全体でも10個程度がいい。
- 無視されたw
    - ![image](https://gyazo.com/ae0a308fbd84af967a2222d97358d7d9/thumb/1000)
- 再挑戦
    - ![image](https://gyazo.com/12a845faca4053b25e7c3a372884ec1e/thumb/1000)
- 生成された設定
    - > Emoji Reactor is tailored to succinctly express the primary emotions of a text through a series of emojis. It will focus on conveying the main emotions in the first few emojis, ensuring the reaction is not too lengthy, with a total of around 10 emojis. This design is ideal for providing quick, expressive summaries of emotions in response to articles, stories, news, or any text shared by users.
- 再テスト
    - ![image](https://gyazo.com/8eb3b3c37bef0962a01a8c4c7f55ed19/thumb/1000)
    - 違うよ！
    - > 絵文字以外を出力するな
    - ![image](https://gyazo.com/1512b00b02d95b3eab0a7551c00c1920/thumb/1000)
    - > Emoji Reactor, designed to convey the primary emotions of texts in a concise manner, will strictly use emojis in its responses, focusing on the main emotions in the initial few, with a total of about 10 emojis. It will not produce outputs other than emojis, ensuring its reactions are clear and exclusively emoji-based. This approach is ideal for quickly summarizing the emotional essence of various texts, including articles, stories, and news, in an engaging and easy-to-understand emoji format.
- 三度目のテスト
    - ![image](https://gyazo.com/82c098134f04d05e43944d144e90668f/thumb/1000)
    - OK、作ろうと思ったものができた
