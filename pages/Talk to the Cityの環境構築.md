---
title: "Talk to the Cityの環境構築"
---

2024-11-28
[https://github.com/takahiroanno2024/anno-broadlistening](https://github.com/takahiroanno2024/anno-broadlistening)

---

[[Talk to the City]]の環境構築
README [https://github.com/AIObjectives/talk-to-the-city-reports/tree/main/scatter](https://github.com/AIObjectives/talk-to-the-city-reports/tree/main/scatter) に書いてある

`$ cd scatter`
`$ python3 -mvenv venv`
`$ . venv/bin/activate`
`$ pip install -r requirements.txt `


下記はまとまってない
- 6/23時点でのラフなメモ
    - Python3.10にしないといろいろトラブル踏むような気がする
    - この環境構築の難しさはデジタル民主主義の普及の妨げになるので解決したい(多様な市民がこのツールを使えることが好ましい)





# Python3.11でのトラブル
READMEには
> We recommend to use python 3.10+ and install the dependencies as follows:
って書いてるけどPython3.11でdistutilsがなくなるのでここでこける

`$ pip install --upgrade pip setuptools`
をして

requirements.txtを一部修正したら動いた
:

```
numpy>=1.25.2
tiktoken>=0.5.1
```



# つづき
`$ python -c "import nltk; nltk.download('stopwords')"`

`$ cd next-app`
`$ npm install`

ここで脆弱性が検知されるので
`$ npm audit fix --force`
もやるといい

# やってみる
`$ cd pipeline`
- さっき`cd next-app`したから`cd ../pipeline`だね
`$ export OPENAI_API_KEY = sk-...`
- もちろん本物のKEYが必要
- `=`の前後にスペースがあるとダメな環境もあるのでは？
`$ python main.py configs/example-polis.json`

# Python3.11でのトラブル
tenacityが3.11対応してないらしい?
[https://github.com/langchain-ai/langchain/issues/22972](https://github.com/langchain-ai/langchain/issues/22972)
8.4.0だとエラーになる
pip install tenacity==8.1.0

これlangchainの出来立てほやほやのバグ！
