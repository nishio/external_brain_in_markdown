
[[ChatGPT API]]
- 2023-03-01 [Introducing ChatGPT and Whisper APIs](https://openai.com/blog/introducing-chatgpt-and-whisper-apis)
    - 公式も[[ChatGPT API]]と呼んでる
- が、実はtext-davinci-003からgpt-3.5-turboに移行できる
    - > システム全体の最適化により、12月以降ChatGPTは90%のコスト削減を達成し、現在その削減分をAPIユーザーに還元しています。...
    - > 本日リリースするChatGPTモデルファミリー「gpt-3.5-turbo」は、ChatGPT製品で使用しているものと同じモデルです。価格は1kトークンあたり0.002ドルで、既存のGPT-3.5モデルよりも10倍安くなっています。また、チャット以外の多くのユースケースに最適なモデルです。初期のテスターは、プロンプトをほんの少し調整するだけでtext-davinci-003からgpt-3.5-turboに移行しています。
- チャット専用なのではなくtext-davinci-003ができてたことが全部できる([doc](https://platform.openai.com/docs/guides/chat))
    - > Although the chat format is designed to make multi-turn conversations easy, it’s just as useful for single-turn tasks without any conversations (such as those previously served by instruction following models like text-davinci-003).
- 全部1/10に値下がりするというのが産業的インパクトのでかい出来事だと思う。「チャットのAPIが生えた、チャットできるぞー」みたいに捉えられるのは微妙〜