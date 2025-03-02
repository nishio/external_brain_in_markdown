
質問して言語化を促す[[かんがえをひきだすチャットボットKeichobot]]を[[GPT-3.5-Turbo]]で実現する実験([[Keichobot on GPT-3.5-Turbo]])の過程で生まれた会話ログ

要約(これもTurboが作った)
- タスクリストの詳細な情報が必要
- タスクの目的を明確化する質問やdoneの定義の質問などを行う必要がある
- チャットボットを使って質問できるタスクリストの管理機能の開発を考える
- ユーザに「やらなきゃいけないけどやる気が出てなくて先延ばしにしてるタスク」を入力させ、ネクストアクションを明確化するための質問をする。

<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> あなたはこの会話で何がどうなるとよいのでしょう？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> AIがタスク管理をしてくれたらいいんじゃないかなと漠然と思ってるのでもっと詳細になるといい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> タスク管理をするAIがあったら、具体的に何をして欲しいかを具体的に考えてみると良いでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> TODOリストって1行1タスクで書いてしまいがちで、そのフォーマットの影響でタスクの実行に十分な文脈を保持できず、時間が経つとタスクの実行が困難になるように思う、これをなんとかしたい
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> なるほど、TODOリストのような形式ではタスクの文脈が抜け落ちてしまうため、それを解決するためのAIの機能について考えてみますか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 一覧性を高くするためにはコンパクトなリストである必要があるが、一つのタスクに注目した時には詳細な情報が必要。この詳細な情報がすでに書かれているならすぐに見れるビューがあるべきだし、ないなら言語化を支援する必要がある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 具体的に、現在のタスク管理の問題点は「TODOリストには詳細な情報がなく、文脈が抜け落ちてしまうことがある」ということであって、その問題点を解決するAIの機能について考えたいということでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> そう、タスクのブレイクダウンとか、ネクストアクションを決めるとか、そもそもなんのためにそれをやるのかとか、doneの定義は何か、とか。1行1タスクのリストでは情報が足りない。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 「1行1タスクのリストでは情報が足りない」という問題を解決するために、タスクのブレイクダウンやネクストアクションの決定、目的の明確化、回避策の定義など、より詳細で文脈を持った情報を提供するAIを実現するためにはどのような機能が必要でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> AIが情報を提供するんじゃない。それは人間の中にあるか、まだないかのどちらかで、人間が見つけ出して言葉にする必要がある
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> ご指摘の通り、AIが情報を提供するのではなく、人間がタスクの詳細や文脈を見つけ出し言葉にする必要がありますが、それに必要な情報を獲得するためには、どのような質問が役立つのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 「これをやることであなたは何がどうなると良いのですか？」これはタスクの目的を明確化する質問。「これはどうなったらひと区切りつくのですか？」これはdoneの定義の質問。「どうすれば完了ですか？」だと、とても遠いゴールを答えてしまうので、区切りを聞くと良い。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> このタスクをやる意味はなんですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 僕がこのタスクをやる意味か。それは自分自身のタスク管理がもっとスムーズになると自分がもっと生産的になって嬉しいし、それが自分以外にも使えるシステムになると世の中の他の人に対しても良い貢献になるから。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> そのタスク管理がスムーズになるために、具体的に何をしたいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 自分や他の人が手軽に使えるシステムになるといい。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 何をシステムとして手軽に使えるようにしたいですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> タスクに関して質問をするチャットボットかな。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> チャットボットに関して、どのような質問をできるようにしたいのですか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> まずタスクリストを与えて、それからそのタスクリストについて質問をできるようにしたい。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> タスクリストについて質問するチャットボットを実装するためには、どのような機能が必要でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> タスクリストの管理機能かな。APIでチャットボットが読み書きアウトライナーがあればそちらにデータの保持を任せるのも手だと思う。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> チャットボットがタスクリストの管理機能を与えられた場合、具体的にどのような操作ができるようになるのでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> タスクリクトを読んで、それについて質問をする。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> タスクリストの内容について、どのような質問をしましょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 最初の一歩をどうするか、ということか。確かにそこは具体的になってないな。もっと具体的に、たとえばタスクリストに「確定申告」とだけ書いてあることを想定してみよう。
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 「確定申告」というタスクについて、どのような質問をしましょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 「どうすれば完了ですか？」「eTaxで提出したら完了です」
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 「eTaxで提出するために必要な手続きを教えてくださいか？」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> eTaxのページを開いて、求められている情報を入力することが必要
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 「入力する情報について、どのような項目がありますか？」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> 収入と支払者情報と経費
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> ユーザーが述べた「収入と支払者情報と経費」という情報について、より具体的にどのような情報が必要でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> うーん。質問が微妙だけど、要するに支払者ごとに金額と名称と所在地が必要だったはず、詳しいことはeTaxのサイトをみないと思い出せない
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 「支払者ごとに必要な金額や名称、所在地の情報はeTaxサイトのどこで確認できますか？」
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> なんとなく「あの辺のボタンを押せば出てくる」と思ってるけど明確に説明できない。それを確認するのをネクストアクションにするのもいいかもね。タスクに対する質問としては「ネクストアクションは何ですか？」と聞いて、それが不明確な時には明確になるまで周辺的な質問をするのが良い
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> 質問が不明確な場合は、タスクに対する質問として「ネクストアクションは何ですか？」と聞き、それが不明確な場合には、明確になるまで周辺的な質問をすることが良いでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/> そうではない。まずユーザに「やらなきゃいけないけどやる気が出てなくて先延ばしにしてるタスク」を入力させる。次に「このタスクのネクストアクションは？」と聞く。だいたいそういう状態のユーザはネクストアクションをわかってないので答えられない。そしたら「思いついたら教えて」と言って、他の質問をしてタスクを明確にしていく。ユーザは色々話してるうちにネクストアクションを思いつくので「じゃあそれをやりましょう！」と返す
<img src='https://scrapbox.io/api/pages/nishio/nisbot/icon' alt='nisbot.icon' height="19.5"/> ユーザが達成したい「やらなきゃいけないけどやる気が出てなくて先延ばしにしてるタスク」に対して、具体的に何をしたいですか？

