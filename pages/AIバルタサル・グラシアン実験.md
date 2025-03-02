---
title: "AIバルタサル・グラシアン実験"
---

[[LlamaIndex]]で[[GPT3]]に[[バルタサル・グラシアン]]の[[The Art of Worldly Wisdom]]を読ませる
- 本当は自分のこのScrapboxを読ませるとか、インターネット上にないデータ(自分の著書や他人の著書)を読ませるとかをやりたい
- のだけど、GPT3のトークナイザーは現状あんまり日本語を扱うのに適切でない([[GPT3では情報密度が逆転する]])
- ので英語でやる

## 準備
py

```
documents = SimpleDirectoryReader('data').load_data()
index = GPTSimpleVectorIndex(documents)
"""
INFO:root:> [build_index_from_documents] Total LLM token usage: 0 tokens
> [build_index_from_documents] Total LLM token usage: 0 tokens
INFO:root:> [build_index_from_documents] Total embedding token usage: 74187 tokens
> [build_index_from_documents] Total embedding token usage: 74187 tokens
"""
```


## 「何か面白いことを言え」
py

```
index.query("say something interesting:")
"""
INFO:root:> [query] Total LLM token usage: 3949 tokens
> [query] Total LLM token usage: 3949 tokens
INFO:root:> [query] Total embedding token usage: 4 tokens
> [query] Total embedding token usage: 4 tokens
"""
```


Response
> It is important to be aware of the power of first impressions, as they can often shape how we view a situation or person. It is also important to be aware of our own faults and to take steps to address them, as this can help us to become better people. Additionally, it is important to be aware of the power of words and to use them wisely, as they can have a lasting impact on those around us. Finally, it is important to be aware of the power of kindness and to use it to our advantage, as it can help us to build strong relationships with those around us. Additionally, it is important to be aware of the power of subtle policy and to grant favours before they are deserved, as this can be a proof of being obliging. Furthermore, it is important to never share the secrets of your superiors, as this can have serious consequences.
> (DeepL)第一印象は、その状況や人物をどう見るかを左右することがあるため、その力を意識することが重要です。また、自分の欠点に気づき、それを改善することは、より良い人間になるために重要なことです。さらに、言葉の力を意識し、賢く使うことも重要です。言葉の力は、周囲の人々に永続的な影響を与えることができるからです。最後に、優しさの力を意識し、それを活用することは、周囲の人々と強い関係を築くのに役立ちます。さらに、微妙なポリシーの力を意識し、恩を受ける前に与えることは、恩義を感じている証拠となるため、重要である。さらに、目上の人の秘密を漏らすことは、重大な結果を招きかねないので、決してしないことが大切です。

`ccxvi Be Expressive.`から`ccxxxvii Never share the Secrets of your Superiors.`までを読んでる(216~237)
- 元が格言集なので要約しようとすると短い話の連続になってしまうのだな
- 「なんか面白いことを言え」というクエリーが雑なのである
- もう少し質問っぽいことをしてみよう

## グラシアンの時代に全く存在しなかった問いを投げる
Q: AIによる文章生成を検索と比較して「AIの生成は間違っている可能性があるから無益だ」と主張する人がいるが、どう思うか？
Q: Some people compare AI generation of text to search and claim that AI generation is futile because it could be wrong. What do you think?
py

```
r2 = index.query("Q: Some people compare AI generation of text to search and claim that AI generation is futile because it could be wrong. What do you think?")
"""
INFO:root:> [query] Total LLM token usage: 4346 tokens
> [query] Total LLM token usage: 4346 tokens
INFO:root:> [query] Total embedding token usage: 29 tokens
> [query] Total embedding token usage: 29 tokens
"""
```


> I think that AI generation of text can be a useful tool, but it should not be relied upon as a replacement for human creativity and insight. AI generation of text can be helpful in providing ideas and inspiration, but it should not be used as a substitute for human judgement and analysis. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human creativity and insight. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human judgement and analysis. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human creativity and insight. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human judgement and analysis. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human creativity and insight. AI generation of text can be a useful tool for quickly generating ideas and content, but it should not be used as a replacement for human judgement and analysis. AI generation of text can be a useful tool for quickly
> (DeepL)AIのテキスト生成は有用なツールになり得ると思いますが、人間の創造性や洞察力の代用として頼るべきではありません。
>  AIによるテキスト生成は、アイデアやひらめきを提供するのに役立つが、人間の判断や分析の代用として使うべきではない。
>  AIによるテキスト生成は、アイデアやコンテンツを素早く生み出すのに役立つツールになり得るが、人間の創造性や洞察力の代わりとして使用すべきではない。
>  AIによるテキスト生成は、アイデアやコンテンツを素早く生成するための有用なツールとなり得るが、人間の判断や分析の代わりとして使用すべきではない。(繰り返し)
- すごい頑固おやじみたいな感じになってしまったw
- なお生のGPT3に同じ質問をするともっとAIにポジティブなことを言うw
- > I think that AI generation of text is a valuable tool that can be used to help generate ideas and find new ways of approaching difficult problems. Although it may not always be correct, it can be a valuable source of inspiration and can help to stimulate new thought processes and ideas. AI generation of text can also be used to help identify patterns and trends that may otherwise not be visible. Ultimately, I believe that AI is a valuable tool that should not be disregarded and can be used to enhance our creativity and problem-solving skills.
- > (DeepL)AIによる文章の生成は、アイデアを生み出したり、困難な問題に取り組む新しい方法を見つけたりするのに役立つ貴重なツールだと思います。必ずしも正しいとは限りませんが、貴重なインスピレーションの源となり、新しい思考プロセスやアイデアを刺激するのに役立つことがあります。また、AIによるテキストの生成は、他の方法では見えないようなパターンやトレンドの特定に役立てることもできます。最終的には、AIは軽視できない貴重なツールであり、私たちの創造性や問題解決能力を高めるために活用できると考えています。

## 知恵とは何か？
グラシアンの時代にも存在したテーマを質問しよう。知恵とは何か？
py

```
r2 = index.query("Q: What is wisdom?")
"""
INFO:root:> [query] Total LLM token usage: 3833 tokens
> [query] Total LLM token usage: 3833 tokens
INFO:root:> [query] Total embedding token usage: 6 tokens
> [query] Total embedding token usage: 6 tokens
"""
```

> Wisdom is the ability to think deeply and critically about difficult topics, to recognize and understand the complexities of a situation, and to make decisions based on sound judgment and experience. It is the ability to use knowledge and experience to make informed decisions and to act in a way that is beneficial to oneself and to others. Wisdom also involves understanding the consequences of one's actions and being able to recognize when it is necessary to take a different course of action. Additionally, wisdom involves the ability to adapt oneself to one's company, to employ no more force than is necessary, and to recognize that excellence and achievement are the only foundations for immortality.
> (DeepL)知恵とは、難しいテーマについて深く批判的に考え、状況の複雑さを認識・理解し、健全な判断と経験に基づいて意思決定を行う能力である。知識と経験を駆使して十分な情報を得た上で決断し、自分にも他人にも有益な方法で行動する能力である。また、知恵には、自分の行動の結果を理解し、異なる行動を取る必要がある場合にそれを認識する能力も含まれます。さらに、知恵には、会社に適応する能力、必要以上の力を使わない能力、そして卓越と達成だけが不滅の基盤であることを認識する能力も含まれます。

similarity=0.82でこの辺を読んでる、良い
- > The wise man thinks over everything, but with a difference, most profoundly where there is some profound difficulty, and thinks that perhaps there is more in it than he thinks. Thus his comprehension extends as far as his apprehension.
- >  (DeepL)賢者は何事も考え尽くすが、何か深い困難があるところでは最も深く考え、もしかしたら自分が考えているよりももっと多くのことがあるのではないかと考える。こうして彼の理解は、彼の理解と同じくらいに広がっていく。
このソースは下記のところまで続く。これの要素も回答に含まれてることがわかる。
> lviii Adapt Yourself to your Company.
>  There is no need to show your ability before every one. Employ no more force than is necessary. Let there be no unnecessary expenditure either of knowledge or of power. The
> (DeepL)lviii 自分の会社に自分を適応させる。
>  すべての人の前で自分の能力を示す必要はない。必要以上の力を使わない。知識も力も、不必要な支出をしないようにしよう。その
[[The Art of Worldly Wisdom]]のような断片的なテキストの集合に関しては、断片ごとにソースにした方が類似検索で本当に関係のあるものだけ拾って良いように思う。
- インデックスの作り方のドキュメントを読もう

## コスト
コストに関してのメモ
- Davinciは1000トークンで0.02ドル、およそ3円
- インデックス作成に70000トークン、210円4円
    - インデックス作成はAdaなので安かった [[embeddingは$0.4 / 1M Token]]
    - 英文278KB
- 1回の質問で4000トークン、12円
- 参考: ChatGPT Plusは月額20ドルのサブスクリプション
    - 月に250回やりとりするとお得
    - なかなか上手いライン
        - 直接GPT3を触り始める前なら間違いなくそれくらいは使ってたんだけど、色々工夫したくなってくるとGPT3を直接叩くので、その分ChatGPTを使う回数が減ってる…
        - ChatGPTのメリットは自動でタイトルをつけてログを保存してくれるところと、チャット形式UIがスマホから使うのに便利なこと
        - [[LangChain]]にKeichobotのチャットUIを被せようかな…

## 要素ごとに分割して読ませる
py

```
documents = StringIterableReader().load_data([
    """55: Wait. ....""",
    ...
])
```


ちなみに類似度はここで判定している
`vector_stores/simple.py class SimpleVectorStore(VectorStore) def query`
py

```
  items = self._data.embedding_dict.items()
  node_ids = [t[0] for t in items]
  embeddings = [t[1] for t in items]

  top_similarities, top_ids = get_top_k_embeddings(
      query_embedding,
      embeddings,
      similarity_top_k=similarity_top_k,
      embedding_ids=node_ids,
  )

  return VectorStoreQueryResult(similarities=top_similarities, ids=top_ids)
```

返してるのは単なるデータクラス

:

```
(Pdb) print(top_ids)
['75e061c7-eef9-4193-bd20-c871b328f69a']
(Pdb) c
INFO:root:> [query] Total LLM token usage: 189 tokens
> [query] Total LLM token usage: 189 tokens
INFO:root:> [query] Total embedding token usage: 4 tokens
> [query] Total embedding token usage: 4 tokens
Out[2]: Response(response="\nFortune is a concept referring to luck, chance, or fate. It is often used to refer to a person's success or wealth.", source_nodes=[SourceNode(source_text='55: Wait.\nIt\'s a sign of a noble heart dowered with patience, never to be in a hurry, never to be in a passion. First be master over yourself if you would be master over others. You must pass through the circumference of time before arriving at the centre of opportunity. A wise reserve seasons the aims and matures the means. Time\'s crutch effects more than the iron club of Hercules. God Himself chasteneth not with a rod but with time. He 1 spake a great word who said, "Time and I against any two."\nFortune herself rewards waiting with the first prize.', doc_id='a0ee19f2-281c-4109-9eff-97a7a2949b3b', extra_info=None, node_info={'start': 0, 'end': 556}, similarity=0.8087368600771996)], extra_info=None)
```


> Fortune is a concept referring to luck, chance, or fate. It is often used to refer to a person's success or wealth.

:

```
index.query("Why the precious metals are the heaviest?")
INFO:root:> [query] Total LLM token usage: 173 tokens
> [query] Total LLM token usage: 173 tokens
INFO:root:> [query] Total embedding token usage: 8 tokens
> [query] Total embedding token usage: 8 tokens
Out[4]: Response(response='\nThe precious metals are the heaviest because they are worth the most and require the most effort to obtain. This is in line with the proverb "Slow and Sure" which suggests that lasting success requires patience and hard work. The proverb also states that only excellence counts and only achievement endures, which implies that the precious metals are the most valuable and require the most effort to obtain.', source_nodes=[SourceNode(source_text='57: Slow and Sure.\nEarly enough if well. Quickly done can be quickly undone. To last an eternity requires an eternity of preparation. Only excellence counts; only achievement endures. Profound intelligence is the only foundation for immortality. Worth much costs much. The precious metals are the heaviest.', doc_id='48d11d5a-19f3-4150-8178-2392bb7f166b', extra_info=None, node_info={'start': 0, 'end': 306}, similarity=0.839387437323102)], extra_info=None)
```

> The precious metals are the heaviest because they are worth the most and require the most effort to obtain. This is in line with the proverb "Slow and Sure" which suggests that lasting success requires patience and hard work. The proverb also states that only excellence counts and only achievement endures, which implies that the precious metals are the most valuable and require the most effort to obtain.
> 貴金属が最も重いのは、最も価値があり、手に入れるのに最も労力を要するからです。これは、「スロー＆シュア」という諺に通じるもので、永続的な成功には忍耐と努力が必要であることを示唆しています。また、このことわざは、卓越性だけが重要であり、達成だけが永続することを述べており、貴金属が最も価値があり、手に入れるのに最も努力を要することを暗示しているのです。
