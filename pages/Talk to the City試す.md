---
title: "Talk to the City試す"
---

> [nishio](https://x.com/nishio/status/1796156174250734034) 文化庁が収集した[[AIと著作権に関するパブリックコメント]]をAI(Talk to the City)で分析可視化しました
>  ![image](https://gyazo.com/513b9a5424f8f2b112bd9305ed5677dd/thumb/1000)
> [nishio](https://x.com/nishio/status/1796156300189208780) 右上の国旗アイコンで日本語に切り替えられます
>  [https://nishio.github.io/tttc_aipubcom_japan/](https://nishio.github.io/tttc_aipubcom_japan/)



実験プロセス
---

[[Talk to the City]]
[/tkgshn/台湾の同性婚に関する議論をTalk to the Cityでレポート化してみる](https://scrapbox.io/tkgshn/台湾の同性婚に関する議論をTalk to the Cityでレポート化してみる)

2024-05-27
- 2024-05-26に[[Talk to the Cityのクラスタリング]]のアルゴリズムが気になったので調べた #都知事選xデジタル民主主義
- [https://github.com/AIObjectives/talk-to-the-city-reports.git](https://github.com/AIObjectives/talk-to-the-city-reports.git)
- ビジュアルツールの"[[Talk to the City Turbo]]"の使用にtkgshnが苦労してたが、CLIのツール"[[Talk to the City Reports]]"もあるみたいなのでこれをみてみよう
- パイプラインは一本道

試すデータを検討する
- [[AIと著作権に関するパブリックコメント]]
    - 割とゴミゴミしてるな...

先に別件で[[東京大学谷口研究室・朝日新聞社共同調査]](UTAS)のPolis的分析をやる
- Polis的データと自然文の両方がある
    - 自然文は少ない
    - まずはPolis的分析をした ✅[[pPolis2024-05-27]]

2024-05-30
UTASデータから自然文を抜き出す
- [https://gist.github.com/nishio/de629941b5ac4a080fae88348df1499c](https://gist.github.com/nishio/de629941b5ac4a080fae88348df1499c)
    - 憲法改正についての126人の政治家のコメント
        - 重複も多い
        - 重複を除くと85件
    - 参議院に関してのコメントだともっと多い

とりあえず小さいもので試すか。[[スモールスタート]]
READMEに従ってcomment-idとcomment-bodyをもったCSVとconfigを作り実行する

# extraction
extraction

```
Running step: extraction
 50%|██████████████████████████████████████████████████████                                                      | 2/4 [00:05<00:05,  2.92s/it]JSON error: Expecting value: line 1 column 1 (char 0)
Input was: 外国勢力の進行に対する厳罰
Response was: I'm sorry, but I can only assist in English. If you provide the text in English, I'll be happy to help you refine it.
Retrying...
 75%|█████████████████████████████████████████████████████████████████████████████████                           | 3/4 [00:07<00:02,  2.51s/it]JSON error: Expecting value: line 1 column 1 (char 0)
Input was: 統治機構改革
Response was: I'm sorry, but it seems like the text "統治機構改革" is in a language that I am not able to understand. Could you please provide the text in English so that I can assist you with making it more concise and easy to read?
Retrying...
JSON error: Expecting value: line 1 column 1 (char 0)
Input was: 統治機構改革
Response was: I'm sorry, but it seems like the text "統治機構改革" is in a language other than English, and I am unable to provide a concise and clear argument based on it. If you could provide a translation or more context, I would be happy to assist further.
Retrying...
JSON error: Expecting value: line 1 column 1 (char 0)
Input was: 統治機構改革
Response was: I'm sorry, but it seems like the text you provided is not related to the topic of artificial intelligence. Could you please provide an argument related to AI for me to help you refine?
Retrying...
JSON error: Expecting value: line 1 column 1 (char 0)
Input was: 統治機構改革
Response was: I'm sorry, but it seems like the text "統治機構改革" is in a language other than English. Could you please provide a translation or more context so I can assist you better?
Silently giving up on trying to generate valid list.
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4/4 [00:12<00:00,  3.23s/it]
```


日本語からの解釈に戸惑ってる
何回かリトライしてダメだったら諦めるのか "Silently giving up on trying to generate valid list."
とはいえ他のコメントも日本語だけどすんなり解釈されてるので、短すぎたり曖昧だったりして意味の抽出に失敗してるってことなんだな。
- 🤖「"統治機構改革"って、どういう意味なのかよくわかんないなぁ〜」

# embedding
embedding

```
Running step: embedding
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 1/1 [00:10<00:00, 10.26s/it]
```


# clustering
:

```
Running step: clustering
Traceback (most recent call last):
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/nltk/corpus/util.py", line 84, in __load
    root = nltk.data.find(f"{self.subdir}/{zip_name}")
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/Users/nishio/talk-to-the-city-reports/scatter/venv/lib/python3.12/site-packages/nltk/data.py", line 583, in find
    raise LookupError(resource_not_found)
LookupError: 
**********************************************************************
  Resource stopwords not found.
  Please use the NLTK Downloader to obtain the resource:

  >>> import nltk
  >>> nltk.download('stopwords')
```


いやいやダメだろこれw
clustering.py

```
   stop = stopwords.words("english")
   vectorizer_model = CountVectorizer(stop_words=stop)
```


言語が英語であることを想定してハードコードされてるじゃん
まあいいか、まずは最後まで進んで全体像を把握するか

:

```
Running step: clustering
OMP: Info #276: omp_set_nested routine deprecated, please use omp_set_max_active_levels instead.
2024-05-30 14:43:23,417 - BERTopic - Reduced dimensionality
2024-05-30 14:43:23,423 - BERTopic - Clustered reduced embeddings
```


# labelling, takeaways, overview
:

```
Running step: labelling
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3/3 [00:02<00:00,  1.20it/s]
Running step: takeaways
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 3/3 [00:04<00:00,  1.67s/it]
Running step: overview
```


# translation
:

```
Running step: translation
Translating to Mandarin...
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 7/7 [00:16<00:00,  2.38s/it]
Translating to English...
  0%|                                                                                                                    | 0/7 [00:00<?, ?it/s]JSON error: Expecting ',' delimiter: line 1 column 216 (char 215)
Response was: ["Through public debate, considering Japan's history and education, it is necessary to create a democratic law by taking time into account.", "It is important to reflect the public opinion by creating a process of "constitutional amendment" through consensus.", "It is necessary to stop the annual budget system.", "For the protection of human rights, it is essential to have discussions and collaborations on the internet.", "Through public debate, considering Japan's history and education, it is necessary to create a democratic law by taking time into account.", "By passing the process of "constitutional amendment", reflecting the public opinion is important.", "For Japan to consider Japan's future, it is necessary to establish a law that will become the basis.", "By revising the 41st article of the constitution, implementing the national referendum, and reflecting its contents in politics is important.", "Keep an eye on the "constitutional amendment".", "Revise the 41st law, implement the national referendum, and reflect its contents in politics."]
Retrying batch...
Warning: batch size mismatch!
Batch len: 10
Response len: 9
Batch item 0: 国民の議論を通じて、日本の伝統や習慣を考慮した自主憲法を時間をかけて作るべき
Response: By engaging in public debate, considering Japan's history and education, creating necessary self-defense laws over time is essential
Batch item 1: 「創憲」のプロセスを通じて国民の意見を反映させるべき
Response: By promoting the principles of 'innovation', reflecting the opinions of the people to be considered
Batch item 2: 廃止すべき予算の単年度制度
Response: It is necessary to stop the annual budget system
Batch item 3: 人権保護のためにインターネット上での取り組みが必要
Response: For the protection of human rights, it is essential to have an internet platform for gathering information
Batch item 4: 国民の議論を通じて日本の伝統や習慣を考慮した自主憲法を時間をかけて作るべき
Response: By engaging in public debate, considering Japan's history and education, creating necessary self-defense laws over time is essential
Batch item 5: 『創憲』のプロセスを通じて国民の意見を反映させるべき
Response: Establishing laws to become a better future for Japan that the Japanese people consider
Batch item 6: 日本国民が考える日本の将来のためになる憲法を創設すべきだ。
Response: By revisiting discussions and debates, developing Japan's unique education and history, creating necessary self-defense laws over time
Batch item 7: 国民と議論を重ねながら、日本独自の習慣や伝統を鑑みた自主憲法を時間をかけて作る。
Response: Keep the focus on 'innovation'
Batch item 8: 「創憲」を目指す。
Response: Amend the 41st law, implement national referendums on important legislation, and reflect its contents in politics
Batch item 9: 憲法第四十一条を改正して、重要法案について国民投票を実施し、その内容を政治に反映させるべき。
Retrying with smaller batches...
```

まとめて翻訳しようとして失敗してる
- 何度かやり直してた
- 結果的に翻訳はできたっぽい

# visualization
:

```
Running step: aggregation
Running step: visualization
> next-app@0.1.0 build
> next build
```


静的HTMLが出力される

![image](https://gyazo.com/cd28455301f8f4eb3c034e1b7bf4cf36/thumb/1000)
タイトルはconfigかどこかで設定すべきだったな

> Overview:
>  The public consultation on constitutional development in Japan revealed three main clusters of opinions. Cluster 0 emphasized the importance of crafting a unique constitution reflecting Japanese traditions, while Cluster 1 focused on constitutional reform through public engagement and utilizing the internet for human rights protection. Cluster 2 highlighted the need for a new constitution with amendments to include national referendums and strengthen the role of the National Diet, along with calls for strict penalties against foreign interventions.
<img src='https://scrapbox.io/api/pages/nishio/gpt/icon' alt='gpt.icon' height="19.5"/>概要:
日本における憲法改正に関する公開協議では、3つの主要な意見のグループが明らかになりました。クラスタ0は、日本の伝統を反映した独自の憲法の作成の重要性を強調し、クラスタ1は、憲法改革を公衆の参加を通じて行い、人権保護のためにインターネットを活用することに焦点を当てました。クラスタ2は、国民投票を含む改正や国会の役割を強化する新しい憲法の必要性を強調し、外国からの干渉に対する厳しい罰則を求めました。

![image](https://gyazo.com/44f207f7dba5759da45359d4026c1481/thumb/1000)

ホバーするとこうなる
![image](https://gyazo.com/b4edf6bd8b0ac7ad8c90b4dc959f0bb3/thumb/1000)
クリックするとこうなる
![image](https://gyazo.com/daa59e7c46e449879ef4b650b030aeb0/thumb/1000)

これをこのクラスターに入れるか
![image](https://gyazo.com/b4c0ca19fdd29845366f5e3a00908ed6/thumb/1000)

![image](https://gyazo.com/2d99689ba283be2603326428a2922153/thumb/1000)
翻訳失敗してる

> Representative comments:
>  国民の議論を通じて、日本の伝統や習慣を考慮した自主憲法を時間をかけて作るべき
>  国民の議論を通じて日本の伝統や習慣を考慮した自主憲法を時間をかけて作るべき
>  国民と議論を重ねながら、日本独自の習慣や伝統を鑑みた自主憲法を時間をかけて作る。
>  国民の議論を通じて、日本の伝統や習慣を考慮した自主憲法を時間をかけて作成することが重要です。
>  廃止すべき予算の単年度制度
- これをこのクラスターに入れるか

![image](https://gyazo.com/39cbb634818132cf5507627f6b9c0f5e/thumb/1000)

# Appendix
![image](https://gyazo.com/9d91ba4647492bdea0946b1d67a586bb/thumb/1000)
これは有用だな
- 途中経過データもあるといいのに

AIコスト
![image](https://gyazo.com/c0e35ea852610126fe5e9d8a1bfbb20e/thumb/1000)

データ量
- 日本語2450文字

大きなデータで試す前にもうすこし色々試すか
configを再検討
json

```json
{
  "name": "Recursive Public, Agenda Setting",
  "question": "What should be top of the agenda as humanity develops and deploys artificial intelligence?",
  "input": "UTAS_2022__SQ6_16_FA",
  "model": "gpt-3.5-turbo",
  "extraction": {
    "workers": 3,
    "limit": 12
  },
  "clustering": {
    "clusters": 3
  },
  "translation": {
    "model": "gpt-4",
    "languages": ["Mandarin", "English"],
    "flags": ["TW", "EN"]
  },
  "intro": "This AI-generated report relies on data from the UTAS 2022 (東京大学谷口研究室・朝日新聞社共同調査)."
}
```


- > タイトルはconfigかどこかで設定すべきだったな
    - nameとquestionがそれ
- クラスタ3個に固定してるんだな
- 翻訳の部分、日本語で処理してから英語に翻訳するつもりでこう設定した
    - けど、クラスタリングが英語を仮定しているコードだったのでむしろ英語で処理して日本語に翻訳する方がいいかも
    - 日本語のまま処理したい場合、クラスタリングステップでCountVectorizerを使ってる部分を日本語を想定した形態素解析と日本語のストップワード設定が必要だ
    - extractionのpromptに"All texts should be in English."と追加して英語で抽出する方針で進める

再実行
"外国勢力の進行に対する厳罰"と"統治機構改革"はまた「わからん」と言われてた
あ、日本語に翻訳し忘れた
:

```
So, here is what I am planning to run:
{'step': 'extraction', 'run': False, 'reason': 'nothing changed'}
{'step': 'embedding', 'run': False, 'reason': 'nothing changed'}
{'step': 'clustering', 'run': False, 'reason': 'nothing changed'}
{'step': 'labelling', 'run': False, 'reason': 'nothing changed'}
{'step': 'takeaways', 'run': False, 'reason': 'nothing changed'}
{'step': 'overview', 'run': False, 'reason': 'nothing changed'}
{'step': 'translation', 'run': True, 'reason': 'some parameters changed: languages'}
{'step': 'aggregation', 'run': True, 'reason': 'some dependent steps will re-run: translation'}
{'step': 'visualization', 'run': True, 'reason': 'some dependent steps will re-run: aggregation'}
Looks good? Press enter to continue or Ctrl+C to abort.
```

後半だけやり直してくれる

英語から日本語への翻訳は特に問題なくバッチ処理できていた
![image](https://gyazo.com/df09fdbd0383a3f2ba268babcf4f9a92/thumb/1000)
うーん「創憲」なんて用語は知らないから誤訳される

prompt: `All texts should be in English. Translate Japanese words based on their meaning, not just their sound.`
embeddingでエラー
- `TypeError: expected string or buffer`
- ![image](https://gyazo.com/e14a78aa645250327a5444578f53eb8e/thumb/1000)
これはあれだな
- [FIX: LLM sometimes returns string and the code handle it as list by nishio · Pull Request #186 · AIObjectives/talk-to-the-city-reports · GitHub](https://github.com/AIObjectives/talk-to-the-city-reports/pull/186)

![image](https://gyazo.com/42ad2adc162133c7db85bbcf2040a56f/thumb/1000)
プロジェクトに名前をつけるべきだった



# [[AIと著作権に関するパブリックコメント]]
534365文字
普通にやっても数百円な気がするが、いちおう1/10データで試すか

## extraction
> Input was: 「A 事業者ガイドライン案」 別添1.第1 部関連/P13/20 行目「Al によるリス ク」
> Response was: I'm sorry, but it seems like the text you provided is in Japanese and it's not clear how it relates to the task of refining arguments in English. Could you please provide an argument or statement in English that you would like me to work on?
- これは誤送信かな〜

![image](https://gyazo.com/96d04b3dacc97adfd0532ea689148816/thumb/1000)
意外と安い

`openai.error.InvalidRequestError: This model's maximum context length is 16385 tokens. However, your messages resulted in 17461 tokens. Please reduce the length of the messages.`
これは困るな

色々実験の結果
![image](https://gyazo.com/93fac38b5ca66a3704982db49350eb71/thumb/1000)
そろそろ最終版を作ろう

全部入り
![image](https://gyazo.com/aba0d2524512bed37a47b1f360c3f2a3/thumb/1000)
うーん、企業コメントを入れたらそればかり出るな
- 一般人のコメントが薄すぎる？
- 混ぜた方が面白いかと思ったんだが...

個人からの2013件のデータに限定してみる
`"clusters": 7`にしてみた

![image](https://gyazo.com/03cfc231950f8299513156ac1c034afb/thumb/1000)
うーん、あまり変わらないな

あ、`"extraction" "limit": 12`これか
- 24に変えてみよう

![image](https://gyazo.com/752caf0a8cdf21c1254f4e09eaca97be/thumb/1000)
増えた
しかし`Warning: data for page "/" is 170 kB which exceeds the threshold of 128 kB, this amount of data can reduce performance.`

さらに48に変えてみる

:

```
File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/steps/translation.py", line 102, in translate_batch
    parsed = [a.strip() for a in json.loads(response)]
```

`json.decoder.JSONDecodeError: Invalid \uXXXX escape: line 1 column 1098 (char 1097)`
うーん、これは厄介だな

やり直したら動いた
- リトライの実装が不十分ということかな、未確認

![image](https://gyazo.com/4532c61d6dc74dbbf653aa1481fee36a/thumb/1000)
いい感じ、やっぱりこれくらい点がないと「分布の可視化である」という感じがしないよね
- 右下のクラスタがちょっと離れてる感とか

extructionのlimitを上げると点が増えていくということは、序盤で「組織からのデータを混ぜると組織からの意見ばかりピックされるなぁ」となったのは、単に組織からの意見だけでlimitに達したということかも

日本語2450文字のUTASのデータと534365文字のAIパブコメのデータでどっちも数セントしかかかってないのは、limitに当たってるからか。
実験としてはリミットをもっと大きくしてみるべきだな。
limitを48から10000に増やす。コストとしては7ドルくらいだろう。

走らせてからコードを読んでる
extraction.py

```
   comments = pd.read_csv(f"inputs/{config['input']}.csv")
   limit = config['extraction']['limit']
   comment_ids = (comments['comment-id'].values)[:limit]
```

あー、なるほど、そういうことね
じゃあ2013人分のデータは入れたけどいきなり48人分に減ってるじゃん！

![image](https://gyazo.com/e0e1c18e00f5b575f2fa37ab845b0fd2/thumb/1000)
ここまできて死んだ
:

```
 99%|███████████████████████████████████████████████████████████████████████████████████████████████████████▏| 666/671 [29:36<00:13,  2.67s/it]
Traceback (most recent call last):
```

`openai.error.InvalidRequestError: This model's maximum context length is 16385 tokens. However, your messages resulted in 19680 tokens. Please reduce the length of the messages.`

185001345000002001以降のデータに関してフォーマットが変わったのかCSV抽出のタイミングで結合されてるな
それを手で削って1997件にすると動きそう
しかしまあこう言うサイズ超過がないかは技術的には実際にAPIを叩く前にチェックできるわけだし、超過のエラーメッセージはもう少しデバッグしやすくした方がいいな

[[Polisは意見のクラスタリング、TTTCはトピックのクラスタリング]]

無事進んでる
:

```
100%|██████████████████████████████████████| 666/666 [30:12<00:00,  2.72s/it]
Running step: embedding
100%|██████████████████████████████████████| 6/6 [00:15<00:00,  2.65s/it]
Running step: clustering
OMP: Info #276: omp_set_nested routine deprecated, please use omp_set_max_active_levels instead.
2024-05-31 04:37:45,187 - BERTopic - Reduced dimensionality
2024-05-31 04:37:45,284 - BERTopic - Clustered reduced embeddings
Running step: labelling
100%|██████████████████████████████████████| 7/7 [00:04<00:00,  1.74it/s]
Running step: takeaways
100%|██████████████████████████████████████| 7/7 [00:16<00:00,  2.35s/it]
Running step: overview
```


> 185001345000002001以降のデータに関してフォーマットが変わったのかCSV抽出のタイミングで結合されてるな
結論、3つ目のPDFから`●受付番号`の前に空白がついたりつかなかったりしている
- `●受付番号`で始まることを区切り条件としていたため、結合されてしまったものがあるということ
- 直した、2985件ある

:

```
 93%|██████████████████████████████████████       | 556/601 [1:33:50<07:35, 10.13s/it]
Traceback (most recent call last):
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/steps/translation.py", line 102, in translate_batch
    parsed = [a.strip() for a in json.loads(response)]
                                ^^^^^^^^^^^^^^^^^^^^
...
json.decoder.JSONDecodeError: Unterminated string starting at: line 1 column 382 (char 381)
```

いやいやマジかよ

これと同じ原因
- > `json.decoder.JSONDecodeError: Invalid \uXXXX escape: line 1 column 1098 (char 1097)`
- > うーん、これは厄介だな
- > やり直したら動いた
- > リトライの実装が不十分ということかな、未確認
流石に1時間半実行してこけたからやり直しってのは...

一旦翻訳をOFFして最後までやってみよう
![image](https://gyazo.com/3812304949fb72e6d10c8414abb84422/thumb/1000)
![image](https://gyazo.com/cad9b3292c1e806ab450e1e9f2682291/thumb/1000)

例えばこれで「クラスタ数をもっと多くしてみよう」とかやった場合に、翻訳はやり直されるのか？
- クラスタの要約文などは再生成されるから再翻訳が必要だと思うが、extractionの結果はそうではないよな
- キャッシュされて再利用されるべきだと思うが、その仕組みはあるかな

「後5分で翻訳が終わるから、終わったらデプロイして寝よ」と思ってたら中国語翻訳のフェーズが始まった(あと1時間ちょい) 寝よ

2024-05-31
![image](https://gyazo.com/29a6818e0bb23986f1992c5ab5766713/thumb/1000)
できた

色々トラブったりやり直したりしたけども、想定金額に収まってるな
![image](https://gyazo.com/a1b1c1f9c32359eef0543505a5e202b5/thumb/1000)

> 「クラスタ数をもっと多くしてみよう」とかやった場合に、翻訳はやり直されるのか？
:

```
% python main.py configs/aipubcom.json                       
(!) {'step': 'clustering', 'filename': 'clusters.csv', 'dependencies': {'params': ['clusters'], 'steps': ['embedding']}, 'options': {'clusters': 8}} step parameter 'clusters' changed from '7' to '50'
diff_params ['clusters']
So, here is what I am planning to run:
{'step': 'extraction', 'run': False, 'reason': 'nothing changed'}
{'step': 'embedding', 'run': False, 'reason': 'nothing changed'}
{'step': 'clustering', 'run': True, 'reason': 'some parameters changed: clusters'}
{'step': 'labelling', 'run': True, 'reason': 'some dependent steps will re-run: clustering'}
{'step': 'takeaways', 'run': True, 'reason': 'some dependent steps will re-run: clustering'}
{'step': 'overview', 'run': True, 'reason': 'some dependent steps will re-run: labelling, takeaways'}
{'step': 'translation', 'run': True, 'reason': 'some dependent steps will re-run: labelling, takeaways, overview'}
{'step': 'aggregation', 'run': True, 'reason': 'some dependent steps will re-run: clustering, labelling, takeaways, overview, translation'}
{'step': 'visualization', 'run': True, 'reason': 'some dependent steps will re-run: aggregation'}
Looks good? Press enter to continue or Ctrl+C to abort.
```

翻訳は変わる部分だけで済むみたい

:

```
100%|████████████████████████████████████████████| 606/606 [2:31:52<00:00, 15.04s/it]
Translating to Taiwan...
  9%|█████████                                                                                              | 53/606 [08:00<1:13:18,  7.95s/it]
```

え？2時間半かけて翻訳し直してるみたいだけど？ww

:

```
100%|███████████████████████████████████████████████████▊| 605/606 [1:38:47<00:09,  9.80s/it]
Traceback (most recent call last):
  File "/Users/nishio/talk-to-the-city-reports/scatter/pipeline/steps/translation.py", line 119, in translate_batch
    return translate_batch(batch, lang_prompt, model, retries - 1)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
...        
RecursionError: maximum recursion depth exceeded
python main.py configs/aipubcom.json  56.16s user 33.46s system 0% cpu 4:13:37.44 total
```

なんだこれ [full stacktrace](https://gist.github.com/nishio/b5e54d84a080fa7397559f32ee48dc84)
4時間かかった上で確率的にしか発生しないエラーで失敗してるな
![image](https://gyazo.com/08143c5154dee81bf134625d3c8f31f4/thumb/1000)
コストはそんな高くないんだけど
そもそも今回のクラスタ数を変えただけのシチュエーションで4時間かけて翻訳が走るのは何か間違ってるし
確率的に発生するトラブルのケアが足りてないのでデータが大きくなるほどやりなおしになる確率が高まる

![image](https://gyazo.com/c9a671b43b4488ac2c82390ac847e3d3/thumb/1000)
日本語版の翻訳は済んでるけど台湾版でこけたので日本語訳のデータもない
50クラスタに分けたものは色々個性的で面白い
このそれぞれのクラスタから1個の賛否分かれる問いを作ってPolisするとかも面白いかも

今後の方向性
- 日本語の入力で日本人向けに出すレポートに関して、現在内部で一旦英語にしているのを、英語にせずに日本語のまま実行可能にする
- 翻訳のスクリプトをもう少し改善して、まず翻訳なしで英語でクラスタを確認するところまでやってから、追加で日本語、…と後から言語を増やせるようにする
- 2000人文のパブコメで5000データポイントとか作られて、それが全部プロットされてる現状では2万人のデータを処理することは困難、前段階でクラスタリングを掛けて似た意見を一つにまとめる


2024-06-03
[[Talk to the CityでPlurality本の内容を可視化]]
![image](https://gyazo.com/516d87e486692d3102793a8b5b27461e/thumb/1000)
えー、こういうゴミが生成されてしまった時にフィルタするには...
- 公式の手軽な方法はなさそう

`embedding.py``にフィルタを書き加えて強制再実行する

util.py

```
    for (i, option) in enumerate(sysargv):
        if option == '-f':
            config['force'] = True
        if option == '-o':
            config['only'] = sysargv[i + 1]
        if option == '-skip-interaction':
            config['skip-interaction'] = True
```


あー、だめだ、ここはチェックされちゃうのか
`ValueError: Make sure that the embeddings are a numpy array with shape: (len(docs), vector_dim) where vector_dim is the dimensionality of the vector embeddings. `

手前のargs.csvを書き換えるしかないか
filter_argument.py

```
import pandas as pd

# Load the arguments from the CSV file
arguments = pd.read_csv("outputs/plurality/args.csv")

# List of arguments to ignore
ignores = ["error", "argument", "reference", "references", "source", "sources", "message", "contributions"]

# show size
print(len(arguments))

# Filter out the ignored arguments
filtered_arguments = arguments[~arguments['argument'].isin(ignores)]

# show size
print(len(filtered_arguments))

# write filtered_arguments to output/plurality/args.csv
filtered_arguments.to_csv("outputs/plurality/args.csv", index=False)
```


`arguments_array.shape=(3497,), embeddings_array.shape=(3353, 1536)`
argsを更新したのになぜか再実行されてないな、再度-oでforceする。
`arguments_array.shape=(3497,), embeddings_array.shape=(3497, 1536)`
できた

おおー、よくなった
![image](https://gyazo.com/fe17a549997d15573ac078150958add6/thumb/1000)
リリースした
[https://nishio.github.io/tttc_plurality/](https://nishio.github.io/tttc_plurality/)

2024-06-17
> Encountered 15 files that should have been pointers, but weren't:


