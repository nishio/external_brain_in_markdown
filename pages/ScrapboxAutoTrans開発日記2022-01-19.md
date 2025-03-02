---
title: "ScrapboxAutoTrans開発日記2022-01-19"
---

prev [[ScrapboxAutoTrans開発日記2022-01-17]]

どう翻訳する？
- アクセスがあったときにまだ翻訳されてないなら翻訳する
- タイトルだけ翻訳する
- まず全部翻訳する

結局、リンクがつながるためには最低限タイトルの翻訳が必要だし、検索のためには全部の翻訳が必要だし、全部翻訳すれば良いのでは？という感じ

こういう流れかな
- 一部翻訳する
    - 観察する
- JSONで書き出す
- 全部翻訳する
    - しばらく運用して観察する
- 更新を検知して自動で再翻訳するようにする

一部翻訳する
- [[DeepL REST API]] #DeepL
- [DeepL Pro | Translate Text, Word Docs & Other Docs Securely](https://www.deepl.com/pro#developer)
    - ![image](https://gyazo.com/2ebfb7ef54b85892f8c9741e74b238fd/thumb/1000)
- [https://www.deepl.com/docs-api/accessing-the-api/](https://www.deepl.com/docs-api/accessing-the-api/)
    - Pythonの公式ライブラリはあるけど将来的にVercel上でTypeScriptでAPI叩くからな
    - どうせRESTで叩くだけだし
- source_lang: "JA"
- target_lang: "EN-US"

split_sentences	Optional	Sets whether the translation engine should first split the input into sentences. This is enabled by default. Possible values are:
- "0" - no splitting at all, whole input is treated as one sentence
- "1" (default) - splits on punctuation and on newlines
- "nonewlines" - splits on punctuation only, ignoring newlines
- For applications that send one sentence per text parameter, it is advisable to set split_sentences=0, in order to prevent the engine from splitting the sentence unintentionally.
ほー、なるほど。文章途中で改行されてるかどうか。Webインターフェースから使ったときに、固定文字で改行されてる系の文書は改行を消さないとうまく翻訳されないなと思っていたが、こういうことか。

preserve_formatting	Optional	Sets whether the translation engine should respect the original formatting, even if it would usually correct some aspects. Possible values are:
"0" (default)
"1"
The formatting aspects affected by this setting include:
Punctuation at the beginning and end of the sentence
Upper/lower case at the beginning of the sentence
これがScrapboxの翻訳に影響するかどうかは要実験

glossary_id	Optional	Specify the glossary to use for the translation. Important: This requires the source_lang parameter to be set and the language pair of the glossary has to match the language pair of the request.
あ、訳語の指定もできそうだ

XMLのハンドリングは公式にサポートされているので、構造を壊さずに翻訳したいなら手元でXMLに変換すると良い

---
できた
![image](https://gyazo.com/a80b6ef2e227460f5c8d2d06bf20b7d1/thumb/1000)

ts

```typescript
const data = {
  auth_key: secret,
  text: text,
  source_lang: 'JA',
  target_lang: 'EN-US',
}
const trans = await fetch('https://api-free.deepl.com/v2/translate', {
  method: 'POST',
  headers: {
    'Content-type': 'application/x-www-form-urlencoded;charset=UTF-8',
  },
  body: new URLSearchParams(data),
})
const transJson = await trans.json()
```


![image](https://gyazo.com/629af2874dc7894f8c9008253c621d46/thumb/1000)
- この試行錯誤だけで無料枠の1%を消費してる

API経由で翻訳するのができた
- ただし今はリクエストごとに翻訳しているのでこのまま公開すると課金が大変なことになるw
- キャッシュする仕組みを作る必要がある

翻訳結果をどうキャッシュするのか考えているうちにこんがらがってきた…

キャッシュするベータベースの設計は、それがどう使われるのかによって決まる
- 日本語タイトルでインデックス張るのか、翻訳後の英語タイトルでインデックスを張るのか
    - 翻訳結果として同じ文字列になるケース
    - 翻訳が変わるケース
- 「どう使われるのか」がまだ不明瞭
    - A: 英語話者が日本語プロジェクトに書かれた内容を1日遅れ程度で英語機械翻訳で読めるようにしたい
        - 英語で検索したときにヒットするようにしたい
        - 社会的トリガー
    - B: 西尾個人が、途中まで英訳している「エンジニアの知的生産術」の翻訳の続きをする助けになる
        - 何がどうなれば助けになるのか不明瞭
        - 「これをやれば読む人がいる」と思えることが大事
    - C: 英語話者が書籍のように英訳版エンジニアの知的生産術を読めるようにする
        - これは機械翻訳ではなくScrapbox Readerで目次を再現だ
    - D: 非英語話者が英語版からの機械翻訳でエンジニアの知的生産術を読めるようにする
        - これはScrapbox Readerからならいけると思う
    - E: エンジニアの知的生産術の増補版を書く
        - Scrapboxの話、RegroupやKozanebaの話、Keichobotの話
        - 過去の記事と接続したい
        - 特にKozanebaの説明は英語で書きたい
        - 多分日本語でScrapboxに書いて、機械翻訳で質が不満なら英訳するって感じかと

あれ？機械翻訳の前に「Scrapboxにおいたコンテンツで書籍的ナビゲーション」をやるべきか？？

![image](https://gyazo.com/f0c5e7b6460222ce91e0d6d661234beb/thumb/1000)


next [[ScrapboxAutoTrans開発日記2022-01-20]]
