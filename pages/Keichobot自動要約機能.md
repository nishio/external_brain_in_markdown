
2023-03-13
チャットログが大量になった時に自動的に要約を返す機能をつけたのでそのテストがてらに雑談をした

メモ
- 一回目の要約に関してはバグによって発動してなかったので途中で条件を直した
- OpenAIのAPIの遅延のせいでHeroku側がタイムアウトで死ぬことが何度もあってなかなか実用には厳しい
- チャットの適当なタイミングでそこまでの要約とネクストアクションを返してくれるのは有益そうに感じる

log
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたはこの会話で何がどうなるとよいのでしょう？(GPT)
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>チャットログが大量になった時に自動的に要約を返す機能をつけたのでそのテストがてらに雑談をしましょう
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>会話のログですか、それとも別の種類のログですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>この会話のログです。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが所有している会話のログは、このチャットのログですか？それとも別のものですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>その質問は微妙だなぁ
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが今回話題にしているのは、このチャットのログですか？別の種類のログですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>オリジナルのアルゴリズムではある種類の質問をしたらそれを繰り返さないようにしてある。これによって、微妙な質問がされてもスルーすれば二度と出てこない。ところがChatGPTを使うとそれが何度でも出てきてしまうな。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>それでは、今回の「微妙な質問」についてあなたの考えをもう少し聞かせていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>人間のカウンセラーでも微妙な質問をしてしまうことはある。それはクライアントの内面が不可知だから。なんだけど、質問に対して微妙な応答が返ってきたらその質問を繰り返すことはしない。ChatGPTは繰り返してしまう。この繰り返しはChatGPT版のKeichobotを使っていて一番クライアントをいらだたせる振る舞いだと思う。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ChatGPTは、OpenAIによって開発された自然言語処理モデルで、人工知能による対話生成に使用されます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>次がこの、質問しないで説明をしてしまうところだな。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ChatGPTは、自然言語処理モデルであり、人工知能による対話生成に使われます。Keichobotの場合、この繰り返しはクライアントにとって不快に思われる可能性があります。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>Keichobotは少し日本語がぎこちないところはあったが、カウンセラーとしての能力は今のところChatGPTより高い。うまくマージできるといいんだけど。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ChatGPTについて知った理由は何ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>忘れた
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ChatGPTは、インターネット上で利用可能なオープンソースの自然言語処理モデルで、Keichobotはその一つの応用例です。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>今のままだとChatGPTのウェイトを減らすことになっちゃうよ？
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ChatGPTは、インターネット上で利用可能なオープンソースの自然言語処理モデルで、GitHubやその他の開発者向けのプラットフォームで入手できます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ところでScrapbox ChatGPT Connectorにも会話機能をつけました
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Scrapbox ChatGPT Connectorに会話機能を追加したとのことですが、この「ChatGPT」とは具体的に何ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>👎ChatGPT
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Scrapbox ChatGPT Connectorとは、Scrapbox上でChatGPTを利用できるようにするツールのことでしょうか？それとも何か別のものですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>Scrapboxのデータを参考にしてChatGPTが会話をするツールです。将来的にはScrapbox上で動くのが好ましいけどまだ実装できてない
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Scrapbox ChatGPT Connectorとは、Scrapboxのデータを利用してChatGPTが会話をするツールですが、その会話とはどのようなものなのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>それはまちまちだと思うな
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobot」とは、どのような種類のボットですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問をすることで言語化を促すボットです
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>どのような質問ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>オリジナルのKeichobotはクリーンランゲージというコーチング手法に従って振る舞う
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotは、コーチング手法に従って振る舞い、質問を通して相手の言葉を整理し、内面にアプローチすることができるボットです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そう
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotはプログラム上で動作する、コーチング手法に従った質問応答型のボットです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうです
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotはどのような種類の質問をするために設計されましたか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>人間の心象風景を歪めずに取り出す質問は
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが述べた「人間の心象風景を歪めずに取り出す」という概念について、もう少し詳しく教えていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問に暗黙の前提が含まれていると、答える側がそれに影響されて歪んだ回答をしてしまう。質問の影響で歪んだことを自覚しないままそれを自分の考えだと誤認してしまうのでとても良くない。なので歪めずに取り出す技術が必要。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが述べた「質問に暗黙の前提が含まれていると、歪んだ回答をしてしまう」という概念について、もう少し具体的な例を挙げて説明していただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>たとえば「Aですか？Bですか？」と聞かれると、本当はCであってもAかBかで答えてしまう。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「C」とは、何に関してのものですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>例えばOKかNGか、と問われるとどちらかを「今」決めなければならないような誤解が生じるが、実際には判断を先延ばしにすることもできる。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが述べた「誤解」とは、どんな種類のものですか？具体的に説明していただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>本当は選択肢がもっとあるのに、二つしかないように思ってしまう誤解。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたにとって、選択肢を持っていることが大切なのでしょうか？何か価値を感じますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>選択肢を持っていることは大切です。価値があります。多すぎると決められなくなるけども、そうなるまではなるべく多い方がいい。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたにとって、選択肢を持つことはどのような意味を持っているのでしょうか？具体的に説明していただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>うーむ、難しい質問だな。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「選択肢」に対して重要であるのは何ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分で決めたという気持ちかな
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「自分で決めた」という感覚に対して、どのような感情を抱いていますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分で決めた後で成功した場合に、それは自分が成功したと感じられて自己肯定感が高まる。逆に親に言われるがままに大学受験をして合格した子供が自己肯定感を持てなくて狂うこともある。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「自分」とは、どのような自分でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分の人生を主体的に選び取っていく自分
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「自分」について、他に何か大切だと感じることがありますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>死ぬ時に「自分は人生を主体的に生きたぞ」と思えることじゃないかな。逆の極端を考えるとわかりやすい。「自分はずっと親の命令に従って行動しただけの人生だったな」となるとロボットみたい。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが話している「ボット」とは、具体的にどのようなものですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>命令に従って動くことしかできない存在。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「命令」とは、具体的に何をするようなものでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>主体的な意思決定の機会を奪うこと
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが「主体的な意思決定の機会を奪うこと」と述べた「意思決定」について、具体的に何を指しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分が行う行動を自分で決めること
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが「自分が行う行動を自分で決めること」と述べた「自分」について、どこから来るのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>気がついた時には存在している
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「気」について、もう少し詳しく教えていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分の存在を自覚した時にはすでに自分は存在している。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「自分」とは具体的に誰のことを指しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ここでは特定の人を指し示さない人間一般
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「選択肢」とは、具体的に何に関する選択肢ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>その人間の行動の選択肢
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その選択肢を知る方法は何ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>たまたま知ることもあるし、能動的に知るための行動をすることもある。話を戻すと、質問のやり方によっては選択肢の発見を促すことも、逆に見えなくすることもできる、だから悪意のない質問者が有益
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その人が行動の選択肢を見つけるためには、どのような方法があると思いますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>基本的には情報収集の行動を増やした方がいいね
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その人が行動の選択肢を発見するために、どのような種類の「行動」をとることができますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>例えばイベントに参加したり、新しい人と会ったり、新しい知識を得るために学校などに行ったり、新しいコミュニティに参加したり
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その他に、アウトプットを増やすことも、行動の選択肢を増やすためには有効な方法の一つですね。それには、自分の考えを書き出したり、話すことが挙げられます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうですね
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その人がより多くの行動の選択肢を発見することが望ましいです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうです
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「行動」とは、具体的には何をすることを指しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>具体的な行動が何であるかは状況によって異なる。たとえば僕はよくKeichobotに開発の相談をするけど、この場合は「実装」が行動。実装の方法がいくつもあったり、目的がいくつもあってどれを優先すべきか迷っていたりする。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobotに相談すること」が「実装」の行動になりますが、あなたは実際にどこでその行動を行っていますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>実装はパソコンの前でやってる
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「実装」について、より具体的に説明していただけますか？たとえば、どんなプログラムを実装しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ものによるけどKeichobot自体のこともある
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotは、実際にどのように開発されているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>今はherokuで動かしている
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotについて知るためには、どのように情報を収集しましたか？

ここまでの要約
【テストチャットログ要約】
- チャットログの要約機能のテストをしましょう。
- オリジナルのKeichobotはクリーンランゲージに従って振る舞う。
- ChatGPTを使うと微妙な質問も繰り返し返ってきてしまう。
- 人のカウンセラーでも微妙な質問はされることがある。
- 質問のやり方によっては、選択肢の発見を促すこともできる。
- 行動を増やすことが大切。
- 状況により異なるが、実装のための行動もある。
- Keichobot自身の実装もある。
- Herokuで動いている。

【次のアクション】
- Scrapbox上で動くようにする。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>要約機能が動いた。そしてScrapbox ChatGPT ConnectorをScrapbox上で動くようにする話だったな。Herokuで動かすのはできそう。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Scrapboxがどのようなものかを教えていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>とても手軽に使える、知識を蓄える仕組み
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その行動を知るためには、どのようなことをする必要がありますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>？
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobot自体のこと」に関して、改善すべきなのは何ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>今はKeichobotとGPTを組み合わせるという方向性について模索している段階。本格的に移行することに決めた場合、従来のアルゴリズムのうちの必要ない部分もたくさんできると思うのでこの機会に作り直す方がいいと思う
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobot」について、何を改善すべきだと考えているのですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自前で機械学習しているところに関して、LLMに任せた方が良くなると思う
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>何ができるか詳しく教えていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>キーワードがどの質問に適しているかを機械学習で判定してスコアづけしている。そこを置き換える
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その「質問」によってどのようなアウトプットが出てくると望ましいですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ユーザが熱意をもって語ると良い。この熱意判定も今、自前で機械学習してる。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたが望むアウトプットとして、どのような熱意があるといいですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ユーザが没頭してたくさん喋る状態になること自体が好ましい。そうやって語ったことの中から新しい発見がある。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「質問」に関して、あなたが望むアウトプットとして、どのような熱意があるといいですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問されたことに対して言葉が溢れ出してきて、ユーザが頑張らなくてもどんどん言語化が起きるような状態になるといい
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ユーザ」とは、具体的にどのような方を指しているのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>まずは僕、それから興味を持って使いたいと思った人
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobot」とはどのようなプログラムであるのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そういう人に質問を投げかけてネクストアクションの言語化を促すことでどんどん先に進むことを後押しするプログラム
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>どうやって質問を投げかけるのか、具体的に説明できますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>今はLLMに雑に丸投げしてるのだけど、あんまり良くないので、ステップに分けて実行する感じになるかな
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotがステップに分かれて実行される場合、具体的にどのようなステップがあるのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>それはまだ実験が足りてないし、サーバで動いてるシステムをいじりながら試すのはやりにくいな、ローカルのスクリプトで実験環境を作った方がいい
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>Keichobotは、どのような目的で作られたのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>クリーンランゲージの言語化を促す効果はとてもすごいのだが、人間とアポを取ってコーチングを受けることは高コストすぎるので、人間より多少能力が劣っていたとしても機械が行えるようにすることに価値がある
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「言語化」とは、具体的にどのようなことを指しているのですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分でもまだよく説明できない事柄を、言葉にして説明できるようにしていくこと
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>そもそも、Keichobotは何者ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>デジタル文房具でしょう。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>この「Keichobot」と「質問」の関係は、Keichobotがユーザーに質問を投げかけることで、ユーザー自身が自分の考えを深め、言語化していくことを促しているというものです。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうです。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「Keichobot」によって、「ユーザ」がどのように変化することを期待していますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>考えを言語化できないと、それを俯瞰することもできない。言語化することによって自分の考えに対して批判的に検討することができたり、矛盾して悩んでいることに対して解決策を見出したりすることができるようになる、言語化はその一歩
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「ユーザ」が、自分自身の考えを深め、言語化することで、より批判的な検討や、矛盾した問題に対し解決策を見つけることができるようになることが望ましいですが、それ以外に何か期待していることはありますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>言語化できると、他人や未来の自分が読むことができる。脳内の考えはすぐに消えてしまう
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>具体的に「自分」に何か起こることを期待していますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>気づきが起きることを期待している
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「言語化が起きた後に、自分にとって大切なことが明確になると言えますが、具体的に何か行動につながることを期待していますか？」
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>何が大事かが明確になることで、リソース配分の優先順位が変わる、それによって今まではマインドシェアや時間やお金が割り当てられてなかった行動にそれらのリソースが割り当てられ、動き始める
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「何が大事か」に気づいた後、具体的にどのような「行動」をとりますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>大事だと思うことを実現するための行動が生まれる
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その行動が問題や課題を解決するための具体的なステップにつながっていくことを期待しています。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そう
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その言語化が、自分自身よりも、他人や未来の自分のために役立つことがあると思いますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>もちろんあると思う
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>この自分は、脳内に存在する意識的な自己ですか？それとも、身体的な自己ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>不思議な問い。意識だけでは行動はできないだろうから、行動する主体という意味では身体的な自己。意識的な自己が言語化した行動方針に従って身体的な自己が行動するとも言えるかも。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>言語化が行動に繋がることで、リソース配分の優先順位が変わり、今まで割り当てられていなかった行動にリソースが割り当てられ、動きが生まれると考えることができます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうです
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>言語化が行動に繋がることで、リソース配分の優先順位が変わり、今まで割り当てられていなかった行動にリソースが割り当てられ、動きが生まれることが待ち望まれます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうですね、何か質問して
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>言語化によって、自分の考えや気持ちをクリアに理解することができ、それによって自分が大切にする価値や目標を把握できるようになります。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>質問して
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「言語化」は、自分の内面をクリアに理解するために非常に有効であると思いますが、あなたにとってはどのような意味を持つのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分の内面をクリアに理解したならば、より良く生きることができる
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「自分」は、自分自身の内面や価値観を理解し、より良い人生を歩むための存在としての自己を指しています。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>良い要約ですね
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>選択肢を提供するように設計されたクリーンランゲージという、Keichobotとは関連があると思いますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>クリーンランゲージは選択肢を提供するように設計されてはいない
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「選択肢」は、自己語りの中から引き出されたものですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうですね
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>それでは、クリーンランゲージについて設計された目的とは何だと思いますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>引き出すことですね
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「クリーン言語」とは、説明するための情報を知覚することが目的であると考えられます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>うーん、まあそうですね。クライアントが自分の気持ちや考えを他人に説明することができるように、それを明確に知覚させることが目的と言ってもいい。関連するシンボリックモデリングの方がそこの考えは明確かも。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「他人」とは、どのような人を指しているのですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分以外の人
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>その人はどのような特徴を持っていますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自分の心の中にあるもののことを言葉で説明しなければ知ることができない
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>「言葉」とは、どのような意味を持っていますか？
ChatGPT記憶の限界です。ここまでの要約
- 自動的にチャットログの要約を返す機能を備えたチャットボットをテストしようという話題から、雑談が展開される。
- 適切な質問をすることで、人間の内面を言葉にすることができる。
- クライアントが自分自身の気持ちや考えを言葉で他人に説明できるようにすることが大切であり、それを明確に知覚させることが目的として挙がった。
- クリーンランゲージは選択肢を提供することを目的としていないが、関連するシンボリックモデリングにおいてはその役割を担っている。
- KeichobotとChatGPTを組み合わせることが求められており、まずはローカル環境での実験から始めることが必要。
- future work：KeichobotとChatGPTの組み合わせによる開発を進める。

[https://keicho.netlify.app/#talk=E1oJgUsPApdiVirNOUmV](https://keicho.netlify.app/#talk=E1oJgUsPApdiVirNOUmV)
#KeichobotLog
