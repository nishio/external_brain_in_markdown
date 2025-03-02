---
title: "TTTCをColabで動かす"
---

[[Talk to the City]]を[[Google Colab]]で動かすことを試みる

[Talk to the City Scatter on Google Colab](https://colab.research.google.com/drive/1nY5ENhs559f6oKWMa0lqrfsA_1kTm0hd?usp=sharing)

pip installの後で再起動が要求される
- ![image](https://gyazo.com/8f77ea207b32f304ba45378e2dcfa95e/thumb/1000)
- numpyのインストールが原因
- 再起動して先頭から再実行したら動く

OpenAIのAPIキーを環境変数に入れるところと、main.pyが対話的操作を要求してくるところとが面倒だな


OpenAIのAPIキーを環境変数に入れる
- [kaggle - Setting environment variables in Google Colab - Stack Overflow](https://stackoverflow.com/questions/53306150/setting-environment-variables-in-google-colab)
py

```
import getpass, os
OPENAI_API_KEY = getpass.getpass("input OPENAI_API_KEY")
os.environ["OPENAI_API_KEY"] = OPENAI_API_KEY
```

- できた
    - 対話的に聞いてくるので入力する

main.pyが対話的操作を要求してくる
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>Google Colabで実行するツールがPress Enterを要求してくる、どうすればいい？
- <img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>`!echo | <your_command_here>`
- なるほど、できた

実行
- ![image](https://gyazo.com/a72c994b1f56b4bd9a6ceb1b6625ce7a/thumb/1000)
- > Pipeline completed.
- できた

出力された静的HTMLをプレビューするにはどうしたらいいか
- Google Colab上でHTTPサーバを立ててプレビューするのは無茶か
- zipしてダウンロードしてもらう？
    - ![image](https://gyazo.com/9c8b3f803e9b903dbd84b87fafd7b13a/thumb/1000)
    - ダウンロードしても結局ローカルでHTTPサーバを立てないと見れないな...


TTTC2024-08-20
[[サイボウズラボユース夏合宿2024]]


