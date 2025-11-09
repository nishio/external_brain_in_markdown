---
title: "Jigsaw Sensemakerとtttc-light-js勉強会"
---

2025-10-31
- [[サイボウズラボ勉強会]]
- ![image](https://gyazo.com/7b116f8c1e37d85ffcdfb89b9a966ef9/thumb/1000)
- Polisはデータエクスポートができるようになった
    - これを使って色々実験
    - その一つが[[Jigsaw Sensemaker]]

Jigsaw Sensemakerとは
- Googleの子会社Jigsawが公開している「大規模な会話データをLLMで素早く読み解く」ためのツールキット
- オープンソース: [https://github.com/Jigsaw-Code/sensemaking-tools](https://github.com/Jigsaw-Code/sensemaking-tools)
- トピック抽出→発言のトピック分類→要約（合意点・相違点・相対的な合意度）までを自動化
- シン東京2050に相当するような長期計画のブロードリスニングでの立案がアメリカでも行われている
    - [[ボーリンググリーン]]
    - そこで使われているのがJigsaw Sensemaker

Polisからのエクスポート
- 最近のPol.isはレポート欄からexportができる
    - 元データには[[星さんのPRでの議論のPolis]]を使う
        - [https://pol.is/4ewtfar8u5](https://pol.is/4ewtfar8u5)
        - ![image](https://gyazo.com/ec1202442dda15ebbb832de20cf767f1/thumb/1000)
            - 94件の意見に対して176人が6412票を投じていて、一人当たり平均36票

    - ![image](https://gyazo.com/ef36139770250b155f89d0d18120afc1/thumb/1000)
    - ![image](https://gyazo.com/c739caa1068845f8e2582e7cdc8d592d/thumb/1000)
- Sensemakerの結果
    - 94 statements
    - 6,374 votes
        - 少し少ないのは実験データをエクスポートしたのが先週だから
    - 8 topics
    - 27 subtopics
    - [https://nishio.github.io/result-sensemaker-tttc/polis-ja-summary.html](https://nishio.github.io/result-sensemaker-tttc/polis-ja-summary.html)
        - まずここで[[Polis型データ]]を使ったSenseMakerのフルの機能解説
    - テキストからのトピック抽出を使う処理
        - トピック識別 (Topic Identification)
        - 分類 (Categorization)
        - 要約生成 (Summarization)
    - Polis的な賛成反対投票の結果を使う処理
        - Common Ground (共通認識): 高い賛成率のコメント
            - 例:
            - > Common ground: 参加者は、個人の自己決定権を「家族の伝統」よりも優先すべきだと主張しました。
        - Differences of Opinion (意見の相違): 賛否が拮抗するコメント
            - 例:
            - > Differences of opinion: 婚姻制度そのものを性別を問わない「パートナーシップ制度」に再編すべきかという点について、参加者の間で意見が分かれました。
        - Groups (グループ分析): グループ間の意見の違い



YouTubeからの抽出
- YouTubeからはコメントごとの高評価のデータは取れるが、低評価のデータが取れない
    - もし取れる方法をご存知でしたら教えてください。「YouTubeのコメントがなんでも[[Polis型データ]]とみなして分析ツールに入れられる」となったらPolis的なものへの参加ハードルが下がるので社会的インパクト大きい
- 高評価だけを試しに使ってみた
    - が、その方法だと20件以上高評価のあるコメントが全部「コンセンサス」として扱われるし、意見の食い違いは票が40~60%のものを抽出しているので常に0になるので良くなかった
- 投票データを捨ててテキストだけでやった場合
    - SenseMaker [https://nishio.github.io/result-sensemaker-tttc/youtube-no-votes-summary.html](https://nishio.github.io/result-sensemaker-tttc/youtube-no-votes-summary.html)
    - この場合に[[Talk to the City Turbo]]とほぼ同じものになるのではないか、というのが今回試す前の考えを
    - 同一データを元にした両者の結果を確認する
        - tttc-light-js: [https://nishio.github.io/result-sensemaker-tttc/youtube_report_japanese.html](https://nishio.github.io/result-sensemaker-tttc/youtube_report_japanese.html)
        - [[tttc-light-js]]はTalk to the Cityの最新版
            - [AIObjectives/tttc-light-js: An open-source LLM analysis tool to improve collective discourse and decision-making.](https://github.com/AIObjectives/tttc-light-js/)

SenseMakerの処理の流れ
- library/src/tasks/categorization.tsのcategorizeCommentsRecursiveが重要な要素
ts

```typescript
export async function categorizeCommentsRecursive(
  comments: Comment[],
  topicDepth: 1 | 2 | 3,
  model: Model,
  topics?: Topic[],
  additionalContext?: string
): Promise<Comment[]>
```

- 初回呼び出し時に library/src/tasks/topic_modeling.ts の learnOneLevelOfTopics を呼び出し、これがLLMを使ってトピック抽出をしている
- promptはLEARN_TOPICS_PROMPT
    - ざっくり翻訳
    - > 以下のコメントを分析し、共通するトピックを特定してください。
    - >  トピックの粒度を考慮してください。トピックが少なすぎると内容を過度に単純化して重要なニュアンスを見落とすおそれがあり、多すぎると冗長になって全体の構造が不明瞭になる可能性があります。
    - >  過度な詳細に踏み込みすぎることなく、主要なテーマを効果的に要約できるバランスの取れたトピック数を目指してください。
    - >  コメントを分析したのち、その内容を効果的に表現できる最適なトピック数を決定してください。
    - >  また、トピック数が少ない場合になぜ最適でないのか（過度の単純化や重要なニュアンスの欠落の可能性）、トピック数が多い場合になぜ最適でないのか（冗長さや全体構造の不明瞭化の可能性）をそれぞれ正当化してください。
    - >  最適なトピック数を決めた後、そのトピックを特定してください。
    - 1つのプロンプトで「最適なトピック数の決定」と「トピックの特定」をやっている
        - こういうのはreasoning model向きだね
    - 全部のデータを一度にLLMに渡している
    - Q: モデルは何？
        - A: オリジナルのコードは[defaultで"gemini-2.5-pro-preview-06-05"を使ってた](https://github.com/Jigsaw-Code/sensemaking-tools/blob/56bbf62caee5cfbd7b6549eb1cb7bde54c748089/library/src/models/vertex_model.ts#L52C25-L52C55)
            - ドキュメントには[「Gemini-1.5 Proだと1000件で1ドルくらい」みたいなことが書いてある](https://github.com/Jigsaw-Code/sensemaking-tools/blob/main/README.md?plain=1#L104)
                - > As of April 10, 2025 the cost for running topic identification, statement categorization, and summarization was in total under $1 on Gemini 1.5 Pro.
    - Q: 要約の部分を AI に任せてる以上、モデル自体に政治的な偏りがあったら、結果に影響しそう
        - A: 実際、LLMはリベラル
            - [[Whose Opinions Do Language Models Reflect?]]
        - Q: 政治の世界で AI を使う場合、モデル選定は政府調達基準で、国産のものに限るみたいなことになっていったりするんだろうか
            - A: そういうことをいう人はいるだろうし、「国産に限定されたら性能的に全然ダメ」って反論もあるだろうし、「だから国産LLMを作る必要があります！予算くれ！」って意見もあるだろうし、どうなっていくんでしょうね
            - 個人的には「国産LLMの性能が見劣りする状況」が解決する前に「国産に限定」というルールが決まったら、AIによる世界の高速な進歩に日本が取り残されて、新しい「失われた何十年」が始まると思う
- promptには書いてないが、JSON Schema validationでフォーマットを縛っている
json

```json
[
  { name: "Polisとデジタル民主主義" },
  { name: "生成AI（特にイラスト）を巡る議論" },
  { name: "動画内容や出演者への感想・反応" },
  { name: "SNSとオンラインコミュニケーションのあり方" },
  { name: "入湯税など具体例に関する解説・補足" }
]
```

- そのあと、各コメントをこのトピックに対して分類する
ts

```typescript
// categorization.ts:573
comments = await oneLevelCategorization(comments, model, topics, additionalContext);
```

    - ここでは1095件のコメントを100個ずつの11バッチに分割して実行する
prompt

```
以下の各コメントについて、下記のリストから最も関連性の高いトピックを特定してください。

入力トピック:
${JSON.stringify(topics)}

重要な留意点:
- 割り当てるトピックがコメントの意味を正確に反映していることを確認してください。
- 必要に応じて1つのコメントを複数のトピックに割り当てても構いませんが、可能な限り1つにとどめてください。
- 可能な限り既存のトピックを優先して使用してください。
- すべてのコメントは少なくとも1つの既存トピックに割り当ててください。
- 既存のトピックにうまく当てはまらない場合は「Other」トピックに割り当ててください。
- 入力トピックに記載されていない新しいトピックを作成しないでください。
- JSON出力を生成する際は、レスポンスサイズを最小化してください。たとえば、不要な空白や改行を加えず、次のようなコンパクトな形式を推奨します: {"id": "5258", "topics": [{"name": "Arts, Culture, And Recreation"}]}
```

    - 分類できなかったら3回までリトライして、それでもダメだったやつはOtherにする
    - 分類結果はCommentオブジェクトのtopicフィールドに書く、最初はundefinedで、この時に`{name: string}`になる
- これで1段階の分類ができた
    - categorizeCommentsRecursiveをtopicDepth=2で再度呼び出す
    - level1のトピック情報を使って、まずコメントを絞り込む
ts

```typescript
// このトピックに属するコメントだけを抽出
const commentsInTopic = getCommentTextsWithTopicsAtDepth(comments, topic.name, 1);
// 例: "Polisとデジタル民主主義" → 356件
```

    - このコメント集合に対してサブトピックを作る `learnSubtopicsForOneTopicPrompt`
prompt

```
以下のコメントを分析し、次の上位トピック「${parentTopic.name}」の中に共通するサブトピックを特定してください。
サブトピックの粒度を考慮してください。サブトピックが少なすぎると内容を過度に単純化して重要なニュアンスを見落とすおそれがあり、多すぎると冗長になって全体構造が不明瞭になる可能性があります。
過度な詳細に踏み込みすぎず、主要テーマを効果的に要約できるバランスの取れたサブトピック数を目指してください。

コメントを分析したのち、内容を効果的に表現できる最適なサブトピック数を決定してください。
さらに、サブトピック数が少ない場合になぜ最適でないのか（過度の単純化や重要なニュアンスの欠落の可能性）、多い場合になぜ最適でないのか（冗長化や全体構造の不明瞭化の可能性）をそれぞれ正当化してください。
最適なサブトピック数を決めた後、そのサブトピックを特定してください。

重要な留意点:
- サブトピック名を上位トピックと同一にしないでください。
- ほかのコメント群では別の上位トピックが使われています。以下の上位トピック名はサブトピック名として使用しないでください: ${otherTopicNames}
```

    - 追加で「悪い例」としてサブトピック同士が似すぎているものを例示している
    - このサブトピックに対してまた分類をする
- デフォルトでtopicDepth=2なのでここで終わり
    - topicDepth=3まで一見いけそうなコードだけどClaude Codeは「NestedTopicの型定義が2階層までしか想定してない」と言ってる、実際そう見えるが動くかどうか検証はしてない
        - 今回動かすためにも割といろいろ手直ししたので...
    - Q: レポートの中に"Prominent themes"というsubtopicの下の構造があるように見えるが？
        - ![image](https://gyazo.com/2e95c47c78465bc75f62c5d431373be8/thumb/1000)
        - これは`library/src/tasks/summarization_subtasks/topics.ts`の`getThemesSummary()`で要約文として生成されたもの
prompt

```
すべてのstatementsを対象に、最大5個の顕著なテーマを特定し、簡潔な箇条書きで作成してください。これらのstatementsはすべて${this.topicStat.name}に関するものです。各テーマは、太字の短いテーマ説明で始め、続けてコロンを置き、その後にそのテーマを説明する1文のみを書いてください。以下のCriteriaを満たし、Output Formatを厳密に遵守してください。箇条書きの前にテキストを付けないでください。
<criteria format="markdown">
 * 公平性（Impartiality）: statementsに対する賛否や警鐘などの規範的判断を述べないこと。
 * 忠実性（Faithfulness）: statementsを正確に反映し、虚構や誤解釈を避けること。
   * 同様に、statements間の合意の程度を仮定・誤記しないこと（例：一部のstatementsにしか言及がないのに「全会一致」などと表現しない）。
   * この基準はテーマ名にも適用される：疑いようのない圧倒的合意がない限り、テーマ名に「〜への支持」などの強い合意を示す表現を用いないこと。
   * 具体的であること。「もの」「側面」などの曖昧名詞を避けること。
 * 包括性（Comprehensiveness）: すべての意見を出現頻度に応じて反映すること。ただし、少数意見を絶対に除外しないこと。強い異議や立場の混在がある場合は具体的に含めること。
 * 用語の一貫性（Consistent terminology）: 常に "statements" を使用し、"comments" は使用しないこと。
</criteria>
<output_format format="markdown">
 タイトルケースのテーマ: 文
</output_format>
```


tttc-light-jsの処理の流れ
- Step 1: Comments to Topic Tree
py

```
@app.post("/topic_tree")
def comments_to_tree(
    req: CommentsLLMConfig, ...
) -> dict
```

    - LLMで1発でトピックとサブトピックを作る
    - まずサニタイズしている(Sensemakerはしてない、Claude Code談)(後述)
defaultSystemPrompt

```
あなたはプロのリサーチアシスタントです。多くのパブリック・コンサルテーション、調査、市民アセンブリの運営を支援してきました。興味深いインサイトを抽出することに関して優れた直感を持っています。あなたは Pol.is のようなパブリック・コンサルテーション・ツールに精通しており、他者が投票できるような明確で簡潔な主張を用いて作業することの利点を理解しています。
```

defaultClusteringPrompt

```
コメントのリストを渡します。
これらのコメントに含まれる情報を、関心のあるトピックとサブトピックに分解する方法を提案してください。
トピック名とサブトピック名はできるだけ簡潔にし、短い説明でそのトピックの内容を説明してください。

次の形式のJSONオブジェクトを返してください:
{
  "taxonomy": [
    {
      "topicName": string,
      "topicShortDescription": string（最大30文字）,
      "subtopics": [
        {
          "subtopicName": string,
          "subtopicShortDescription": string（最大140文字）,
        },
        ...
      ]
    },
    ...
  ]
}

では、コメントのリストはこちらです:
\${comments}
```

    - これらのプロンプトが`common/prompts/index.ts`に書かれててAPIのペイロードに積まれてそのままOpenAIに送信されてるので、これは外部に露出したらまずいな
- Step 2: Extract and place claims
    - 各コメントから「主張（claim）」を抽出し、Step 1で作成したトピック/サブトピックに配置する
py

```
@app.post("/claims")
async def all_comments_to_claims(
```

defaultExtractionPrompt

```
参加者が述べたコメントと、すでに抽出済みのトピックおよびサブトピックの一覧を渡します。
参加者が支持し得る、最も重要で簡潔な「主張（claim）」を抽出してください。
関心があるのは、与えられたトピック／サブトピックのいずれかにマッピングできる主張のみです。
主張は十分に一般的でありつつも、陳腐な決まり文句ではないこと。
他の人が反対し得る内容であること。
また、各主張は「原子的（複合せず、一点の立場を表す）」である必要があります。

【抽出ルール（厳格運用）】
1. あいまい・散漫で要点のないコメントからは「主張を0件」抽出すること
2. 一般化に至らない単なる逸話からは「主張を0件」抽出すること
3. 明確で実質的に論争可能な立場が複数含まれる場合は複数の主張を抽出してよいが、類似点は別主張にせず「1つの主張のバリエーション」として扱うこと
4. 本当に論争可能な立場のみを抽出すること
5. 次に挙げるものは抽出しないこと：
   - 紋切り型・自明な言い回し（例：「communication is important」）
   - 立場を伴わない単なる経験の記述
   - 同一の根底アイデアの些細な言い換え
   - 明確な立場のない質問や思索

【品質閾値】
そのコメントに抽出に値する十分な主張があるか確信が持てない場合は、何も抽出しない側に倒してください。
周辺的な主張を拾ってノイズを増やすより、取りこぼしの方が望ましいとします。

各主張については、該当する「引用」も併せて提示してください。
引用は主張を裏付けるのに十分でありつつ、可能な限り簡潔にしてください。
引用は論理的な議論である必要はありません。発言者がその主張をする動機を示す個人的なエピソードや逸話でも構いません。
引用内で重要でない部分は「[...]」を用いて省略しても構いません。

次の形式のJSONオブジェクトを返してください:
{
  "claims": [
    {
      "claim": string, // 非常に簡潔な抽出主張
      "quote": string, // そのままの引用
      "topicName": string, // 与えられたトピック名から
      "subtopicName": string // 与えられたサブトピック名から
    }
  ]
}

ここにトピック／サブトピックの一覧があります:
\${taxonomy}

そしてコメントは次のとおりです:
\${comment}
```

    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>不要なものを抽出しないための予防策がすごい。
        - 相手がLLMだと、結構無理難題も平気でプロンプトに書くんだなあ。
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>このプロンプトも LLM に作らせたのかな？
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>[[プロンプトはLLMに作らせるほうがいい]]
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>どういうプロンプトで、今のロジックのプロンプトを作らせたんだろ？
        - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>それはわからんけど、ちょうど昨日僕がやってたのはこう
            - > なので僕の外部脳を読んだGPT5に考えさせて、そのプロンプトを実際に使って抽出されたものを見てフィードバックを返してアップデートさせた
                - from [[チャットから知見を引き出すシステム#69037b1f0000000000ae2403]]
    - コメントそのままを分類するのではなく「主張の抽出」をするのが独特
        - これは[[Talk to the City Scatter]]の時もまずextraction phaseを持っていた
        - 一方でこのバージョンでは「引用」もセットで抽出している
            - [[Plurality本の概念マップ]]を作った時に僕もやった
            - このデザインは「AIがそう主張する根拠はユーザのこの発言です」とやって手軽に[[どこから来たのかのトレーサビリティ]]ができるのが良い
    - コメントは1つずつLLM処理している
        - SenseMakerが100個ずつ束ねて処理していたのとは違う
        - LLM呼び出し自体は6並列にしている
    - Step1で作られたtaxonomyを元にPydanticでスキーマ定義を作って、それをOpenAIの呼び出し時にJSON Schema validationとして与えている
        - `pyserver/structured_schemas.py`: 構造化スキーマ生成 (L25)
py

```
    TopicEnum = PyEnum('TopicEnum', {name: name for name in topic_names})
    SubtopicEnum = PyEnum('SubtopicEnum', {name: name for name in subtopic_names})

    # Create the Claim model with constrained fields
    Claim = create_model(
        'Claim',
        claim=(str, Field(description="A concise extracted claim")),
        quote=(str, Field(description="The exact quote supporting this claim")),
        topicName=(TopicEnum, Field(description=f"Must be one of: {', '.join(topic_names)}")),
        subtopicName=(SubtopicEnum, Field(description=f"Must be one of: {', '.join(subtopic_names)}")),
        __base__=BaseModel
    )
```

        - 「限られたtopic名から選ぶ」ということをEnumとして表現しているわけ
        - さらにコンテキストにも積んでる
py

```
    # Build prompt with explicit taxonomy constraints
    # This is "belt and suspenders" with structured outputs
    taxonomy_constraints = create_taxonomy_prompt_with_constraints(taxonomy_list)
    full_prompt = llm.user_prompt + "\n\n" + taxonomy_constraints + "\n\nComment:\n" + sanitized_comment
```

        - これの費用対効果がどうなのかは個人的には疑問に思っている
            - まあ大したコストではないから念のためおまじないをするか〜ぐらいの感じなのではと思う
        - 余談だけどプロンプトを`+ "\n\n" +`で組み立てるね
            - SenseMakerでは`<instruction>...</instruction><data><comment>...</comment>...</data>`って感じでXML的プロンプト
            - どちらが良いのかは不明
- Step 3: Sort & Deduplicate Claims
    - 似た意見をまとめる
        - ![image](https://gyazo.com/77dccf9ab1c56997066c096c1d434e2e/thumb/1000)
            - これの+4とかが「5つの意見をまとめました」ということ
    - ソートする
        - claimのソートに関しては数が多い順
        - topic, subtopicのソートは「関与した人が多い順」と「claimが多い順」の2つがあって前者がデフォルト
    - 「似た意見をまとめる」と一言で言うけど実際のプロンプトを見ると結構複雑なことをしている
        - embeddingで近いものをまとめるのとは大違い
defaultDedupPrompt

```
あなたは、今回のコンサルテーションで「どのテーマが最も重要か」を利用者が理解できるように、主張（claims）をグルーピングします。目的は、類似する主張を裏付けのあるグループに統合しつつ、本当に独自の視点は保持することです。

各主張には ID・主張テキスト・引用テキストが含まれます。

グルーピング判断フレームワーク（FRAMEWORK）:

Step 1 - コアテーマの特定:
自問してください：「これらすべての主張に共通して表明されている“3～5個の主なアイデアや懸念”は何か？」
これらを候補グループとします。

Step 2 - グルーピング基準の適用:
次のいずれかを共有していれば、主張を同じグループにまとめます:
✓ 同一の根本的懸念・問題（提案する解決策が異なっていても可）
✓ 同一の提言・解決策（理由づけが異なっていても可）
✓ 表明している価値観・原則が同じ
✓ 同じトピックの異なる側面（例：「コストが高い」＋「価格が不明確」＝価格に関する懸念）
✓ 一般的なパターンの具体例

以下の場合のみ、主張は別グループのままにします:
✗ このサブトピックの中で、完全に別のトピックを扱っている
✗ 互いに対立する立場（何かへの賛否）が表明されている
✗ 片方はプロセス／方法（how）、もう片方は成果／何を（what）に関するもの

Step 3 - 強いグループ主張（Group Claim）の作成:
各グループについて、次を満たす主張を書きます:
- 共有される本質を、より高い抽象度で捉える
- 元の主張に現れる語彙・概念を用いる（新しい用語の導入を避ける）
- 具体性があり意味のあるレベル（「Xを改善」などの曖昧な常套句は避ける）
- グループ中のすべての引用が妥当に支持し得る
- 明快で平易な言葉遣い
- 参加者の発言内容に忠実である

Step 4 - グループの妥当性確認:
- 目標のグループ数に合わせるよりも、自然な主題的一貫性を優先
- 各グループは明確で意味のあるテーマを表すべき
- 単一主張のみのグループは比較的まれであるべき。多い場合は、主張同士を結びつける上位テーマを見落としていないか再検討する
- 過度な統合は避ける：数を減らすために無理に結合しない
- 適切なグループ数は、入力に含まれる視点の自然な多様性に依存する

良いグルーピング例:

入力主張:
- 「駐車料金が高すぎる」
- 「駐車パスの仕組みが分かりにくい」
- 「駐車スペースを増やすべき」

良いグループ主張: 「駐車のアクセス性と負担可能性の改善が必要」
理由: 3つとも、強調点は違っても「駐車が障壁」という点を扱っているため。

入力主張:
- 「再生可能エネルギーを優先すべき」
- 「市はレジ袋を禁止すべき」

悪いグルーピング: 「環境施策が必要」
理由: どちらも環境ではあるが、政策としては別個に扱うべき。

次の形式の JSON オブジェクトを返してください:
{
  "groupedClaims": [
    {
      "claimText": "このグループの引用すべてを代表できる上位主張",
      "originalClaimIds": ["claimId1", "claimId3", "claimId5"]
    }
  ]
}

では、グルーピング対象の主張はこちらです:
\${claims}`;

export const defaultSummariesPrompt = `
トピックの説明・サブトピック・主張を含む JSON オブジェクトを渡します。
各トピックについて、そのトピックのサブトピックと主張の詳細サマリーを生成してください。
サマリーは140文字以内とします。

次の形式の JSON オブジェクトを返してください:
{
  "summaries": [
    {
      "topicName": string, // 与えられたトピック名
      "summary": string // 最大140文字
    }
  ]
}

では、トピックはこちらです:
\${topics}
```

    - ここ面白い
        - > 同一の根本的懸念・問題（提案する解決策が異なっていても可）
        - チームみらいの[[しゃべれるマニフェスト]]のデータを見て僕が「問題意識を抽出してまとめ直そう」としたのと関連している
        - 同じ問題意識に対する異なる解決策の提案はまとまっていた方が良い
        - 同様に「根拠が異なるが主張は同じ」もまとめるようだ
            - > 同一の提言・解決策（理由づけが異なっていても可）
- 4: 要約
defaultSummariesPrompt

```
トピックの説明・サブトピック・主張を含む JSON オブジェクトを渡します。
各トピックについて、そのトピックのサブトピックと主張の詳細サマリーを生成してください。
サマリーは140文字以内とします。

次の形式の JSON オブジェクトを返してください:
{
  "summaries": [
    {
      "topicName": string, // 与えられたトピック名
      "summary": string // 最大140文字
    }
  ]
}

では、トピックはこちらです:
\${topics}
```

- Step 5: Cruxes (Optional)
    - オプショナルな論点分析
    - 「最も意見が分かれる論点」を発見する実験的機能
        - [[いどばたビジョン]]や[[Cartographer]]っぽさがある
defaultCruxPrompt

```
説明付きのトピックと、このトピックについて異なる参加者が述べた高レベルの主張リストを渡します（参加者は "Person 1" や "A" のような仮名で識別されます）。あなたには、当該トピックに関するすべての発言に基づき、参加者を二つのグループに最もうまく分けられる新たな具体的な文「cruxClaim（分岐点となる主張）」を作成してほしいです。一方はその主張に賛成、もう一方は反対になるようにしてください。理由づけを説明し、参加者を "agree" と "disagree" のグループに割り当ててください。

次の形式の JSON オブジェクトを返してください
{
  "crux": {
    "cruxClaim": string,        // 新たに抽出した主張
    "agree": list of strings,   // cruxClaim に賛成する参加者（与えられた仮名）のリスト
    "disagree": list of strings,// cruxClaim に反対する参加者（与えられた仮名）のリスト
    "explanation": string       // 参加者の視点からこの cruxClaim を統合した理由
  }
}
```



[[トップダウンの分類]]
- LLMベースでの分類は[[AIでKJ法2024-12-19]]とかと関連している
    - 一方で[[KJ法]]の川喜田二郎は「分類してはいけない」と言っている
        - ここの違いを究明していくと面白そう
    - ![image](https://gyazo.com/973ea9617662cabdccfcf594eff6bb7c/thumb/1000)
    - > 大分けから小分けにもっていくのはまったく邪道である。[[かならず小分けから大分けに進まなければならない]]のである。これがこの方法の 決定的な問題点のひとつであ る(第7図参照)。
    - > ...
    - > 自分の心のなかに、「これだけの紙きれの資料は、自分の考えによれば、内容的に市場調査・品質管理・労務管理と三つに大きく仕切るのが正しい」などというたぐいの、グループ分けについての独断的な原理をあらかじめ頭の中にもっているからである。その独断的な分類のワクぐみを適用し、そのできあいのワクの中にたんに紙きれの資料をふるい分けて、はめこんでいるにすぎないのである。これでは KJ法の発想的意義はまったく死んでしま う。
        - [[発想法]] p.77
    - SenseMakerのやり方は右の専制的やり方そのまんまでは？
    - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>KJ法との比較での考察は面白い
        - ボトムアップにしたらいいのかな？
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>似てるものを集めるっていうのをボトムアップでやるっていっても、コンテクキストの容量問題からは逃れられないって話だと解釈 (100 件くらいなら眺められるけど 1000 件は辛いという話)
- どちらもユーザの投稿データをえいやとLLMに投げて分類を取得している
    - SenseMakerは分類できなかったものをOtherにするからまだいいとして
    - tttcは「この分類に当てはまるように意見を抽出せよ」と指示してるからLLMが分類として返さなかったやつはしれっと無視されそうだな
        - 明示的にそのスタンスを取ってる
            - > そのコメントに抽出に値する十分な主張があるか確信が持てない場合は、何も抽出しない側に倒してください。
            - >  [[周辺的な主張]]を拾ってノイズを増やすより、[[取りこぼし]]の方が望ましいとします。
        - 川喜田二郎は激おこすると思うw
        - ユースケースによってはこれがありかなしかは意見が分かれると思う
            - まあ、レポートを人間が見たときの「いい感じ」度合いが大事なら、[[ごちゃごちゃした少数意見は捨てたほうがいい]]とは思う
                - もう少し詳細に言語化すると
                    - データから、そこで「主に話されていたこと」(トピック)が人間の認知キャパシティに収まる程度の量だけ抽出される
                    - 各発言をそのトピックに割り振る
                    - 割り振られなかったものは「[[オフトピック]]」
                    - こう考えると、オフトピックの発言をメインのレポートに入れないのは許容範囲な気もする
                    - オフトピックに分類された発言リストを巻末付録につけてもいいかも？というむしろ集めたデータをオープンデータ化すればいいか？
                - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>これ、そのレポートをその後政治の議論にもっていくソースにするんなら、どうせオフトピックは議論にならないから、ユースケース的には問題ない？
                    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>そうかも
                        - 一方で政治家が特定の支持者からの意見を切り捨ててることが可視化されると(全部に均等にリソースを割り振るのは不可能だからとうぜんそうなるわけだが)嫌がる有権者はいそうだし、有権者に嫌がられることを嫌がる政治家はいそう
                        - なので「出力を市民に見せるかどうか」に大きな分かれ目があり、有用なレポートは少数意見を切り捨てるのだが、市民に見せるレポートには切り捨ててないポーズをするインセンティブが強く働くのだと思う
                        - 2つ下の段落の"「情報を捨てていません」と言えるレポート作成を求めているケース"と関連してそう
            - たぶんこれは[[わかりやすいレポート作成]]と[[創発的なプロセス]]とのトレードオフなのだと思う
                - 創発的なプロセスにおいては「[[既存の枠]]」に収まらないデータに注目することが有用
            - もう1軸ありそうな気がする
                - 「わかりやすいレポート作成」よりも「情報を捨てていません」と言えるレポート作成を求めているケース
                - 「[[霞ヶ関のポンチ絵]]」はそれが目的
                - [[みんなの意見を聞いてます感の演出]]
            - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>「[[文書作成過程で生成された不用知の収集と活用可能性の検証]]」を連想した
                - 確かに、レポートに使われなかった素材断片という意味では近い

細かい話
- tttcのサニタイズ
    - `pyserver/simple_sanitizer.py`
:

```
# 1. プロンプトインジェクション検出（例: "ignore previous instructions"）
# 2. PII検出（メール、電話番号、SSN、クレカ）→ [EMAIL]などに置換
# 3. 長さチェック（10,000文字まで）
# 4. 意味のあるコメントか（3文字以上）
```

- SenseMakerはむしろGeminiのセーフティフィルターを無効化している
ts

```typescript
 // vertex_model.ts:172-193
  const safetySettings = [
    {
      category: HarmCategory.HARM_CATEGORY_HATE_SPEECH,
      threshold: HarmBlockThreshold.BLOCK_NONE,  // ← すべて無効化！
    },
    // ...他のカテゴリも同様にBLOCK_NONE
  ];
```

- 複数クラスタ所属
    - Sensemakerは単一のコメントが複数のクラスタに所属できる、8.5%が複数クラスタ所属だった
    - tttcは単一のコメントから複数の意見が抽出され、それが単一のクラスタに所属する
    - こういうデータは[[境界をまたぐ]]データなので
        - 「[[既存のグループを跨ぐ関係性]]」が大事 from [[KJ法勉強会振り返り勉強会#639abad8aff09e0000818a55]]
- ここまでの調査をClaude Codeにやらせたのの最終レポート
    - SenseMaker: [https://gist.github.com/nishio/0326319b8a47c20dfb5e84e6054a8bcc](https://gist.github.com/nishio/0326319b8a47c20dfb5e84e6054a8bcc)
    - tttc-light-js: [https://gist.github.com/nishio/faeea25d89f998fce0706b3093fde124](https://gist.github.com/nishio/faeea25d89f998fce0706b3093fde124)

ここまでのまとめ
- ![image](https://gyazo.com/7b116f8c1e37d85ffcdfb89b9a966ef9/thumb/1000)
- [[SenseMaker]]や[[tttc-light-js]]は[[Talk to the City Scatter]]や[[広聴AI]]と根本的に異なるパイプライン
    - LLMのコンテキスト幅が広くなったことで可能になった新しい手法だと思う
    - ただしこの新しい手法ではどこにもベクトルが出てこないから散布図は作れない
    - 散布図と散布図ではない階層まとめなどを両方見せると、大体散布図のほうがいいと言われる...
        - <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>「散布図がいい」ではなく「図がいい」のでは？
            - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>そうかも！
- いいとこどりをすることは可能なのだろうか？
- 素朴な方法ではなかなか難しそう
    - SenseMakerで出力されたクラスタで色分けしたembeddingのUMAP
    - ![image](https://gyazo.com/02ae9b383a575e3f4b125c09a231e39d/thumb/1000)
    - 高次元空間では分離していてUMAPで混ざってしまってるのか、そもそも高次元空間でも非分離なのか
        - 埋め込みベクトルの空間はパーフェクトな魔法ではないので、LLM的な意味のクラスタが混ざっててもおかしくはない
    - 実験: 各点の高次元空間におけるk近傍においてクラスタ内の点が占める割合
        - k=15での平均純度
            - HDBSCAN: 純度 71.6% ✓ 比較的分離
            - SenseMakerのTopic:      純度 57.6% ✗ より混在
            - SenseMakerのSubtopic:   純度 22.9% ✗✗ 極めて混在
        - Topicごとの純度の違い（右上グラフ）:
            - ![image](https://gyazo.com/1aae37bac179505d9a1926b140c595ea/thumb/1000)
            - 「入湯税」: 純度77.5%、境界点33.9% → 明確に分離
            - 「生成AI」: 純度76.8%、境界点65.1% → 比較的分離
            - 「Polis」: 純度61.3%、境界点91.6% → 中程度の混在
            - 「動画感想」: 純度44.7%、境界点97.3% → 大きく混在
            - 「SNS」: 純度36.1%、境界点100% → 極めて混在


- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>KJ法的な分類がLLMでできるようになったらいいなあ・・・
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>KJ法で分類して、だけじゃできないのか。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>確かに、前に試したのは1年前だからもうできるようになってるかも
        - そういうLLMによる支援機能を[[Kozaneba]]に追加したいが手が回ってない
- <img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='human.icon' height="19.5"/>そのうちデータ渡して、「Talk To The City 方式で散布図出して」でできるようになるかな。
    - <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>コードが公開されてるから適切な権限があればgit cloneして実行できる
        - pip install可能にしておくといいかもw



logs
- [[pSensemaker2025-10-17]]
- [[pSensemaker2025-10-21]]

2025-10-28
クラスタリング結果をUMAPして観察
- 予想としてはランダムでもないが明瞭分離でもないものになる
- [[高次元空間でクラスタリングしてからUMAP]]
カテゴリのembeddingをconcatする実験
- [[クラスタ解説の埋め込みベクトルをconcatしてUMAP]]

[https://chatgpt.com/share/69007cdb-c414-8011-9eff-aac21e0a0870](https://chatgpt.com/share/69007cdb-c414-8011-9eff-aac21e0a0870)
