---
title: "OpenAI DevDay Keynote(2023-11)"
---

[https://www.youtube.com/watch?v=U9mJuUkhUzk](https://www.youtube.com/watch?v=U9mJuUkhUzk)
この英語の45分の動画を日本人が理解する、という知的生産プロセスの効率化を実験する

YouTubeのTranscriptをコピペする。
- 9000トークンくらいある
- [https://platform.openai.com/tokenizer](https://platform.openai.com/tokenizer)
    - ![image](https://gyazo.com/b5d904533e44b854764d20fdefe0d68d/thumb/1000)

Playgroundでgpt-4-1106-previewに入れる
- defaultでmax lengthが短いので最大にした、4095だった
- [https://platform.openai.com/playground?mode=chat&model=gpt-4-1106-preview](https://platform.openai.com/playground?mode=chat&model=gpt-4-1106-preview)
prompt

```
[SYSTEM] Pick important features from following speech transcript and return bullet lists.
[USER] ...
```

![image](https://gyazo.com/2d1e46d0ea5667d026c7093d85156b42/thumb/1000)

result
![image](https://gyazo.com/f09160f596dd3ffd8949d3a3530aa1c8/thumb/1000)

result

```
- OpenAI DevDay Introduction 
  - Sam Altman welcomed attendees to the first-ever OpenAI DevDay.
  - OpenAI's history and connection to San Francisco.
  - Progress over the past year was highlighted.

- ChatGPT and GPT-4 
  - ChatGPT started as a research preview and evolved with the launch of GPT-4.
  - GPT-4 remained the most capable model available.
  - Launched voice and vision capabilities for ChatGPT.
  - DALL-E 3 released as the most advanced image model.
  - ChatGPT Enterprise introduced for business with enhanced features.

- OpenAI Usage and Growth 
  - 2 million developers on OpenAI's API.
  - Over 92% of Fortune 500 companies use OpenAI products.
  - ChatGPT reached approximately 100 million weekly active users.

- OpenAI’s Direction and Goals 
  - Focus on usability and practical impact of AI products on users' lives.
  - GPT-4 Turbo announced addressing developer feedback with new features.

- GPT-4 Turbo New Features 
  - Expanded context length of up to 128,000 tokens.
  - Better response control with JSON Mode and reproducible outputs.
  - Improved world knowledge with updated knowledge cut-off to April 2023.
  - New modalities like DALL-E 3 and text-to-speech API.
  - Customization via fine-tuning, with a new custom models program.
  - Doubling tokens per minute for established GPT-4 customers.

- Pricing Announcements 
  - GPT-4 Turbo made more affordable with a significant price reduction.
  - Improved affordability expected to drive more innovation and use cases.

- Future Commitments and Partnerships 
  - Ongoing partnership with Microsoft and a commitment to AI safety discussed.
  - The future of AI and agents, gradual iterative deployment emphasized.

- Introduction of GPTs 
  - Customized versions of ChatGPT tailored for specific purposes announced.
  - GPTs allow sharing and discovering ways to use ChatGPT.
  - Users can program GPTs with language, enabling broad accessibility.
  - The GPT store to be launched for public sharing and revenue sharing.

- Assistants API 
  - New API provides persistent threads, retrieval, code interpreter, and function calling.
  - Facilitates building agent-like experiences in apps.

- Acknowledgments 
  - Sam Altman thanked the OpenAI team for their hard work.
  - OpenAI's mission highlighted to revolutionize technology and society through AI, empowering individuals and humanity.
```


DeepL

```
- OpenAI DevDayの紹介 
  - サム・アルトマンは、初めてのOpenAI DevDayへの参加者を歓迎した。
  - OpenAIの歴史とサンフランシスコとのつながり。
  - この1年の進捗がハイライトされました。

- ChatGPTとGPT-4 
  - ChatGPTはリサーチプレビューとして始まり、GPT-4のローンチとともに進化しました。
  - GPT-4は最も高性能なモデルであり続けた。
  - ChatGPTの音声と視覚機能を開始。
  - DALL-E 3を最新画像モデルとして発表。
  - ChatGPT Enterpriseを機能強化し、ビジネス向けに導入。

- OpenAIの利用と成長 
  - 200万人の開発者がOpenAIのAPIを利用しています。
  - フォーチュン500社の92%以上がOpenAI製品を使用。
  - ChatGPTの週間アクティブユーザー数は約1億人に達しました。

- OpenAIの方向性と目標 
  - AI製品のユーザビリティとユーザーの生活への実用的な影響に焦点を当てる。
  - GPT-4 Turboは新機能で開発者のフィードバックに対応することを発表しました。

- GPT-4 Turboの新機能 
  - コンテキストの長さを最大128,000トークンまで拡張。
  - JSONモードと再現可能な出力により、より優れた応答制御を実現。
  - 2023年4月に更新された知識カットオフにより、世界の知識が向上。
  - DALL-E 3や音声合成APIなどの新しいモダリティ。
  - 新しいカスタム・モデル・プログラムによる微調整によるカスタマイズ。
  - GPT-4をすでにご利用のお客様には、1分あたりのトークンを2倍にします。

- 価格に関するお知らせ 
  - GPT-4ターボが大幅値下げでよりお求めやすくなりました。
  - よりお求めやすくなったことで、イノベーションとユースケースの拡大が期待されます。

- 今後のコミットメントとパートナーシップ 
  - マイクロソフトとの継続的なパートナーシップとAIの安全性へのコミットメントについて議論。
  - AIとエージェントの将来性、段階的な反復展開が強調された。

- GPTの導入 
  - 特定の目的に合わせたChatGPTのカスタマイズ版を発表。
  - GPTはChatGPTの使い方を共有・発見できる。
  - ユーザーはGPTを言語でプログラミングでき、幅広いアクセシビリティを実現。
  - GPTストアを開設し、公開と収益分配を行う。

- アシスタントAPI 
  - 新しいAPIは、永続スレッド、検索、コードインタプリタ、関数呼び出しを提供します。
  - アプリでエージェントのような体験を構築することを容易にします。

- 謝辞 
  - Sam AltmanはOpenAIチームの努力に感謝した。
  - OpenAIのミッションは、AIを通じて技術と社会に革命を起こし、個人と人類に力を与えることを強調した。
```


興味のあるところを掘り下げてみよう
prompt

```
I'm interested in Assistants API. Explain it in detail.
```

result

```
The Assistants API is a new offering from OpenAI announced at the DevDay event. Here's an in-depth look at what it entails:

- **Persistent Threads**: This feature allows developers to create a continuous conversation thread for each user interacting with the assistant. Unlike the traditional approach, where you need to resend the entire conversation history with each API call, persistent threads manage the state of the conversation and context for you. This simplifies the development process by allowing a continuous dialogue with the AI without having to manage context windows or the serialization of messages.

- **Retrieval**: Assistants API now has the capability to parse and understand external documents. This feature enables the AI to access additional knowledge beyond the current user messages by ingesting long-form documents or databases. This is useful when the AI needs to reference information not contained in the prompt or its own knowledge base.

- **Code Interpreter**: A feature that expands the capabilities of the AI to write, execute, and even generate code during conversation. This allows developers to create assistants that can perform more complex tasks such as data analysis, calculations, and code generation in real-time, akin to having a Python interpreter right within the chat interface.

- **Function Calling**: The Assistants API enhances function calling abilities by ensuring JSON-valid output and enabling the calling of multiple functions simultaneously. This greatly improves the potential for developers to integrate the AI with APIs and third-party services, allowing for a range of actions and interactions within the application.

- **Multimodal Capabilities**: The Assistants API incorporates OpenAI's new modalities, such as DALL-E 3 for image generation and a new text-to-speech API for generating natural-sounding audio. This integration enables developers to build richer, multimodal user experiences.

- **Developer Dashboard**: The API offers a dashboard where developers can see the steps the tools are taking, which includes executing functions with specified parameters and managing uploaded documents. This feature provides transparency and control, allowing developers to troubleshoot and optimize their assistant's behavior.

- **Simplification and Efficiency**: The Assistants API is designed to streamline the process of building advanced AI assistants. It removes the complexity involved in managing conversation states, chunking algorithm setup, and custom backend systems for knowledge retrieval. This means developers can build sophisticated assistive agents with less effort, lower maintenance, and reduced development times.

- **Integration with Apps**: The Assistants API can be integrated into applications to provide users with an interactive AI that can manage conversations, invoke functionalities of the app, and even take real-world actions based on user requests.

As demonstrated in the event, the Assistants API can be put to practical use in a travel app where it answers user queries about destinations, retrieves book flight details or accommodation reservations, and even performs financial calculations for shared expenses.

The Assistants API is a significant step towards creating AI-enhanced user experiences that are more engaging, intuitive, and powerful. It is intended to help developers create not just chat interfaces, but intelligent agents capable of acting on behalf of the user, ultimately leading to the future of AI agents as envisioned by OpenAI.
```


DeepL

```
Assistants APIは、DevDayイベントで発表されたOpenAIの新サービスです。ここでは、その内容について詳しく見ていきましょう：
 
 - **Persistent Threads**： この機能により、開発者はアシスタントと対話する各ユーザーのために継続的な会話スレッドを作成することができます。APIコールのたびに会話履歴全体を再送信する必要がある従来のアプローチとは異なり、永続スレッドは会話の状態とコンテキストを管理してくれます。これにより、コンテキストウィンドウやメッセージのシリアライズを管理することなく、AIとの継続的な対話が可能になり、開発プロセスが簡素化されます。
 
 - 検索**： アシスタントAPIは、外部ドキュメントを解析して理解する機能を持つようになりました。この機能により、AIは長文のドキュメントやデータベースを取り込むことで、現在のユーザーメッセージ以外の追加知識にアクセスできるようになります。これは、AIがプロンプトや独自の知識ベースに含まれていない情報を参照する必要がある場合に便利です。
 
 - コード・インタープリター**： AIが会話中にコードを書いたり、実行したり、生成したりする能力を拡張する機能。これにより開発者は、データ分析、計算、コード生成など、より複雑なタスクをリアルタイムで実行できるアシスタントを作成できる。
 
 - 関数呼び出し**： Assistants APIは、JSON-valid出力を保証し、同時に複数の関数を呼び出すことを可能にすることによって、関数呼び出し能力を強化します。これは、開発者がAIをAPIやサードパーティのサービスと統合する可能性を大幅に向上させ、アプリケーション内でさまざまなアクションやインタラクションを可能にします。
 
 - **マルチモーダル機能**： アシスタントAPIは、画像生成のためのDALL-E 3や、自然な音声を生成するための新しい音声合成APIなど、OpenAIの新しいモダリティを組み込んでいます。この統合により、開発者はよりリッチでマルチモーダルなユーザー体験を構築することができます。
 
 - 開発者ダッシュボード**： APIはダッシュボードを提供し、開発者は、指定されたパラメータによる関数の実行やアップロードされたドキュメントの管理など、ツールが実行するステップを確認することができます。この機能は透明性とコントロールを提供し、開発者がトラブルシューティングを行い、アシスタントの動作を最適化することを可能にする。
 
 - 簡素化と効率化**： Assistants APIは、高度なAIアシスタントを構築するプロセスを合理化するように設計されています。会話状態の管理、チャンキングアルゴリズムのセットアップ、知識検索のためのカスタムバックエンドシステムに関わる複雑さを取り除きます。つまり、開発者は、より少ない労力、より少ないメンテナンス、開発期間の短縮で、洗練された支援エージェントを構築することができます。
 
 - **アプリとの統合**： Assistants APIをアプリケーションに統合することで、会話を管理したり、アプリの機能を呼び出したり、さらにはユーザーのリクエストに基づいて実際の行動を起こしたりできる対話型AIをユーザーに提供することができます。
 
 イベントで実演されたように、Assistants APIは旅行アプリで実用化することができ、目的地に関するユーザーの問い合わせに答えたり、予約したフライトの詳細や宿泊施設の予約を取得したり、さらには共有する費用の財務計算を実行したりすることができる。
 
 Assistants APIは、より魅力的で、直感的で、パワフルな、AIによって強化されたユーザー体験を生み出すための重要な一歩だ。このAPIは、開発者が単なるチャットインターフェイスだけでなく、ユーザーに代わって行動できるインテリジェントエージェントを作成できるようにすることを目的としており、最終的にはOpenAIが構想するAIエージェントの未来につながるものです。
```



さて、これを踏まえて動画を実際に見てみよう
- 内容がわかってるので1.25倍で聞く

- 「スレッドとメッセージ」という抽象化
    - サーバサイドで永続化される
        - 勝手に最近のものだけダイジェストされるのか、それとも[[MemoChat]]的な仕組みで検索するのか、どっちかな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - 後者であって欲しい
- JSON形式でのアウトプットを「追加レイテンシーなしで」保証
    - がっつりフォーマット保証のファインチューニングを掛けたのだな、失敗確率が無視できるくらい小さくなったのだろう<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 検索のデモはいまいち僕のニーズに合わない(一般ウケするデモにしてあるせい)<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 永続的ストレージがあるスタートフルなAPIを提供したことによってサードパーティデベロッパーの側の実装コストが激減した
    - チャンキングやコンテキスト幅のことを考えなくて良くなった
        - この永続的ストレージの中身は後から取得できるのかな、できないとGDPRに怒られるから多分できるんだろうな<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
            - おーー、デベロッパーダッシュボードでスレッドの一覧が見れてる
- Code Interpreterがintegrateされてることで、自然言語で記述するよりPythonで記述した方が良い処理はPythonで書ける
    - 使えるフォーマットみたらC++とかJavaも含まれてるな...<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>
- 音声の入出力がついたことで印象的なデモができるようになった
    - これを使ってデモをするケースが今後あちこちで見られるようになって世の中の「OpenAIすげー」的な雰囲気を高めるんだろうな、うまい宣伝戦略だ<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>

## Assistants APIを試す
拙著[[エンジニアの知的生産術]]のPDFをUpload, RetrievalをONにしてSave
- 少し時間がかかるのはチャンキングしてベクトルインデックスを構築してるからだろう。
![image](https://gyazo.com/04b3f5bca54454f8ebbe8e72aaf79b30/thumb/1000)
PDFを参照したのかどうかよくわからないので明示的に参照させてみる
![image](https://gyazo.com/3f13cafc2bf284f161243604bf47a09e/thumb/1000)
ちゃんと参照した
- どこを参照したのかを確認できる
    - ![image](https://gyazo.com/9035a9053d0ac580955711bc071fe7d9/thumb/1000)
        - 目次だなw
もっと明示的なリクエストをしてみる
- ![image](https://gyazo.com/ca223615727e5a649af21ba49e830412/thumb/1000)
- もっともらしいことを言ってるな

別の質問
- ![image](https://gyazo.com/6fe155ea2ad2e3b5b1cd74fa07ae8d65/thumb/1000)
- 出典表示のリンクが多分化けててUIで確認できない: `【9†source】`
    - ログ自体には検索結果の情報は来てない
    - リンクが壊れてなければ出典確認がUIからできるわけだから、それを取得するAPIはあるはずだな
        - あー、本来はメッセージにannotationsという形で情報が付与されるのか

感想
- 書籍のPDFを投げつけるだけで永続化されたアシスタントができて、いつでも書籍の内容を踏まえた回答をさせられる、超手軽
    - PDF形式で書籍を買えるかどうかは、「AIに読ませられるかどうか」という形の顧客価値になっていくだろう
- 僕個人の研究目的では細かいところをいじりたいのでちょっと使い勝手が悪いな
    - > [nishio](https://twitter.com/nishio/status/1721800710134915476/quick_promote_web/intro) OpenAI DevDayを見て、MicrosoftがVisual BasicやVisual C++をリリースし、それによって多種多様な「Windows用アプリ」が作られていた時代をのことを思い出した。「AIアプリ」を作るエンジニアの時間的コストがOpenAIなら圧倒的に安いって状況を作ってきたなぁ、と。
    - ウェブサイトを作るのにWordPressを使う的な位置付け

slideの要約をしてみた
- [[生成AI時代のプログラミング教育 つくること・学ぶことの歓びに向かって]]

> [nishio](https://twitter.com/nishio/status/1721857526990586203/quick_promote_web/intro) OpenAI Assistants APIに拙著「エンジニアの知的生産術」を入れて質問。これこそ「書籍を読む方法の効率化」だな感
>  ![image](https://pbs.twimg.com/media/F-VEHiGakAEioDR?format=jpg&name=medium#.png)
