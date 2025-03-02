
2023-03-06
- [[かんがえをひきだすチャットボットKeichobot]]のChatGPT APIを使うバージョンとの会話ログ

## 1行要約
- 自然言語プロンプトで記述するシステムは、一見非エンジニアでも手軽に挙動の改善ができるけど、先にメンテ不能の地獄が待っているので[[回帰テスト]]の仕組みが必要。その回帰テストにも[[LLM]]が必要になる。一方で[[A/Bテスト]]と組み合わせるのも可能性が広がる。


## 要約 ver.1 (人間が修正したもの)
- 自然言語で書かれたプロンプトの改善が必要になる
    - ルールをアドホックに追加する実装が手軽
    - しかし、それにはソフトウェア工学的に問題がある
    - プロンプトを修正した後に、問題が解決したのかと、他の問題が再発していないかを検証する必要がある
- つまり回帰テストが必要である
    - 自然言語の出力に対する回帰テストにはLLMを使う必要がある
- A/Bテストとの組み合わせも有効
    - 自然言語プロンプトの良い挙動をLLMを用いて定義する必要はない
    - が、逆にLLMを使うことによってA/Bテストが対象とできる範囲が広がる


## 要約 ver.1 by ChatGPT
- 自然言語プロンプトの改善が必要
- ルールをアドホックに追加する実装はソフトウェア工学的に問題がある
- 修正後に再発しないか検証する必要がある
- 自然言語プロンプトの良い挙動を定義するためにA/Bテストが有効で、LLMを用いて定義する必要はない
- 新しいアプローチは提案されていない

## 要約 ver.2 by ChatGPT
- システム修正について相談があった
- 修正ルールを追加する実装方法は微妙
- ステップ1: 修正によって好ましくない挙動が発生しなくなったか検証
- ステップ2: 回帰テストで再発を確認
- ステップ3: LLMを使用して機械的に判断するテストを行う
- 修正が必要かの判断には、A/Bテスト的な考え方も有効
- 数量化が困難だった自然言語に対してLLM経由で数量化できるようになる

## log
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたはこの会話で何がどうなるとよいのでしょう？(GPT)
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>話すことで思考を整理したい。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>整理したいという目的を達成するために、具体的なアイデアを形成するためにユーザーの内面の問題を掘り下げるための質問をしましょう。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>🙁
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>あなたは自分の思考を整理したいと思っていますが、何が混乱しているか、何について考える必要があるかを明確にするために質問をすることができます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>自然言語プロンプトで実装されているシステムが好ましくない挙動をした時の修正について
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>どのような挙動が起こったのか、具体的に教えていただけますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>傾聴するためのシステムがユーザの発言を否定しまくった
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>それは嫌な経験だったと感じられるかもしれませんね。その経験から、今後どのような修正点を期待しますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>とりあえず自然言語プロンプトに「ユーザを否定するな」と書き足したのだけど、これはソフトウェア工学的には微妙だなぁと思った
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>確かに、「ユーザを否定するな」という表現は微妙ですね。システムのアルゴリズムを修正することで、それが起きないように改善する方法を探すことができますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>違う、その表現が微妙なのではなく、ルールをアドホックに追加していく実装スタイルは良くないということ。ソースコードが肥大化していって、誰もどれが有益なコードでどれが無益なコードかわからなくなる
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>理解しました。修正について、アルゴリズムに対してユーザの発言で否定的な単語が含まれているかどうかをチェックして、それを避けるようにアルゴリズムを改善することは可能でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>僕が説明しようとしたことの2ステップ先を先回りして話されたw そうなんだけど読者がついてこれないからステップバイステップで行こう。現状の「単純にルールを追加する」はそれによって良くなったのかどうかの検証がされていない。まずその修正によって「好ましくない挙動」が発生しなくなったのか、発生した時のデータを入れて検証する必要がある。これがステップ1
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>了解しました。ステップ1は修正を行った後、「好ましくない挙動」が起こらなくなったかどうかを検証することですね。そのために、どのようなデータを収集すべきでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ユーザの入力とそれに対するシステムの出力。で、ステップ2は「好ましくない挙動」が起こらなくなった後に再発していないことを知るためには回帰テストが必要で、人間が目視で発生してるかしてないかを判断したのではダメだということ。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>了解しました。ステップ2は再発を確認するために回帰テストを行うことですね。具体的に、どのようなテストを実施すべきでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>OKかNGかを人間ではなく機械が判断するテストが必要。しかし今回の場合、出力が自然言語の文章であるから、人間がコードで条件式を記述するのは困難。ここにもLLMを使うしかないと思う。これがステップ3
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>先ほどの話に戻りますが、自然言語プロンプトの修正に関連して、具体的にどのようなテストを実施すれば良いでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>具体的にはgivenな入力に対して現在のパラメータで回答を生成させ、その回答を「この回答はユーザの発言を否定しているか？YesかNoかで答えよ」というプロンプトを与えられたLLMに与え、Noが変えることを検証する
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>おっしゃったテストはシステムが発する回答の否定を判定するようですが、そのようなテスト以外にシステムが回答する際に注意すべきポイントには何があるでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>それはさておき、ここまでの話をまとめて。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>私たちの話のまとめは、自然言語プロンプトの修正が必要だということ、ルールをアドホックに追加することではソフトウェア工学的に微妙なこと、修正するには再発テストが必要で、LLMを使うことが必要であるということだと思います。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>そうですね。で、そこまでできると「良くない挙動」を避けるように自然言語プロンプトを改善することが、きちんと検証しながら実行できるようになる。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ご注意いただきありがとうございます。どのようなお話になりますでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>🙁　ここからがさらに先の整理したい話なのでまずは聞いて。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>かしこまりました、聞き取りました。ご依頼者がより具体的になるためのステップについてこちらから質問をしていきます。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>A/Bテスト的な考え方と繋がるのではないかと思う
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>A/Bテスト的な考え方と繋がることを考える前に、自然言語プロンプトの改善について具体的なアウトプットを持つことの方がまず必要だと考えます。伝えたいことを具体化できるようにするにはどのようなアプローチが必要ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>ユーザの発言を否定しない！
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>申し訳ありませんが、前回の回答は誤りでした。そこで、もう一度お伺いしたいのですが、自然言語プロンプトの改善について、具体的なアウトプットを持つことの方がまず必要だと考えます。伝えたいことを具体化できるようにするにはどのようなアプローチが必要ですか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>🙁　あるプロンプトに対する修正を入れるべきかどうかは、一部のユーザに入れてみて、好ましくない挙動が減るかどうかで判断できるのではないか
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>なるほど、よく考えられたアプローチですね。少数のユーザーを対象として、自然言語プロンプトの修正を行い、その後、好ましくない挙動が減ったかどうかを検証することが良い方法であると考えられます。では、そのためにどのような手順が必要でしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>書いて見て思ったけど少し飛躍があるな。「好ましい」の定義がLLMによるものである必要はない。LLMを使ったシステムでも離脱率やクリック率を使って良いし、ユーザによる明示的な良い悪いフィードバックボタンを置いても良い。そこに「LLMが見て判断する」という新しい定義手段が加わっただけ。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>わかりました。具体的なアウトプットを持つためにA/Bテストを行うというアプローチがありますが、好ましい挙動の定義にはLLMを使う必要はなく、離脱率やクリック率、明示的なフィードバックボタンを使うなどの方法もあります。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>「A/BテストがLLMを使うシステムの改善に有効」ではなく「LLMがA/Bテストの対象を増やすことに有効」が適切か
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>ありがとうございます。もう一度お聞きしたいのですが、「LLMがA/Bテストの対象を増やすことに有効」と言えるでしょうか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>それは言える。なぜなら今まで数量化が困難であった自然言語に対してLLM経由で数量化できるようになるから。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>上手くいろんなアプローチを提示しましたね。では、ここまでで整理されるとより良い方向性、また新しいアプローチはありますか？
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>それはまた今度にしよう。ここまでの会話を箇条書きで要約して。
<img src='https://scrapbox.io/api/pages/nishio/kei/icon' alt='/nishio/kei.icon' height="19.5"/>おっしゃったことをまとめると、自然言語プロンプトの修正には好ましい挙動の定義や対象ユーザーの特定などの具体的なアウトプットが必要であり、A/Bテスト的なアプローチやLLMの使用についての提案もあった。また、質問をする際には、キーコンセプトを探し、それに関連する質問をすることが重要である。
<img src='https://scrapbox.io/api/pages/nishio/human/icon' alt='/nishio/human.icon' height="19.5"/>(できてないな
- <img src='https://scrapbox.io/api/pages/nishio/nishio/icon' alt='nishio.icon' height="19.5"/>要約を生成する機能は別でつけよう

[https://keicho.netlify.app/#talk=8pZW2kyh27C7lgy9VH4v](https://keicho.netlify.app/#talk=8pZW2kyh27C7lgy9VH4v)
#KeichobotLog
